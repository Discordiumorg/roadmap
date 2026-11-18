# Discord vote webhook processing: a practical integration checklist

Maintained by the Discordium team. This guide combines documented Discordium behavior with implementation recommendations for application developers. Review date: 18 November 2026.

## Start with the delivery contract

The [Discord vote webhook documentation](https://discordium.org/developers/webhooks) describes `vote.created`, raw-body HMAC-SHA256 verification and at-least-once delivery. Configure a signing secret and verify it before trusting incoming JSON. The stable `eventId` identifies a vote; `X-Discordium-Delivery` identifies an attempt. Ignore test events for rewards.

Use the official documentation for the current payload, response-code rules and retry schedule. Treat the design below as a suggested application architecture rather than an additional Discordium API guarantee.

## Separate receipt from reward delivery

A useful design has three durable states: received, awaiting fulfillment and fulfilled. This makes a vote visible to support staff even when a downstream Discord or game action is temporarily unavailable.

1. Capture the raw request bytes and verify the signature.
2. Parse and validate the event, listing identity and expected payload version.
3. In a database transaction, insert an inbox record and its pending job. Put a uniqueness constraint on the listing and event ID.
4. Commit before acknowledging receipt. For a duplicate, confirm that the original job exists rather than enqueueing another reward.
5. Let a worker perform the reward and record completion.

Acknowledge only after durable acceptance. A crash between an in-memory queue operation and a database write can otherwise lose the work. Keep retry handling inside the worker separate from webhook receipt.

## Design the reward for retries too

An inbox uniqueness constraint prevents duplicate jobs, but it cannot make a remote side effect atomic. If a worker awards a benefit and crashes before recording completion, the next run may try again.

Prefer a reward operation that accepts an idempotency key or sets a desired state, such as an expiry time, instead of blindly incrementing a balance. When that is unavailable, maintain a reward ledger and a reconciliation procedure. Avoid promising exactly-once fulfillment across systems without a mechanism that supports it.

## Keep command-based claims consistent

The [bot vote verification API](https://discordium.org/developers/vote-checking) reports current eligibility, not lifetime voting history. It requires `votes:read`; bot and game voting windows differ. Your application remains responsible for claims.

If both a webhook and a claim command can grant the same benefit, make them consult the same ledger. Choose and document one claim identity so a user cannot obtain the same benefit through both routes.

## Exercise the failure paths

| Scenario | Expected application behavior |
| --- | --- |
| Same event received twice | One pending job and one benefit |
| Concurrent deliveries | Database uniqueness resolves the race |
| Worker restart after a remote action | Retry or reconciliation avoids an extra benefit |
| Dashboard test event | Delivery checked without granting a reward |
| Wrong listing identity | Event rejected before fulfillment |
| Database unavailable | No success acknowledgement for work that was not stored |

## Leave a useful operational trail

Log event ID, listing ID, processing state and a concise failure category. Keep secrets and unnecessary payload data out of logs. Choose a retention period suited to troubleshooting and the data you actually need.

Before deploying, review token scopes, rotation and listing-specific access in the [Discordium Developer API setup guide](https://discordium.org/developers). Give support staff a way to find a failed job and retry it safely.
