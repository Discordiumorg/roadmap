# Discord bot listing checklist: help people find and evaluate your bot

Published by Discordium.

A useful Discord bot listing answers a practical question: can this bot solve a specific problem for this community? A moderation team, a music community and a small gaming group need different things. Clear descriptions and an installation path make those differences easier to evaluate.

This checklist is for developers preparing a listing and community owners comparing options in a [Discord bot directory](https://discordium.org/bots).

## 1. Lead with the job the bot does

Write one sentence that names the audience and the main task. For example: “A reminder bot for gaming groups that posts scheduled sessions in a Discord channel.”

Then explain three or four concrete capabilities. Mention a limitation when it changes someone's decision. A short, accurate description is more useful than a long list of unrelated tags.

Before publishing, check that each feature in the description works in the current release. Keep planned features in a separate roadmap.

## 2. Explain commands and costs before installation

Say whether the bot uses slash commands, prefix commands or both. Give the reader a starting command and explain what should happen after they use it.

Describe the pricing model in plain language:

- Which features are available without payment?
- Which limits apply to free use?
- Which features require an upgrade?
- Where can someone read the current pricing?

If a feature depends on another service or a separate subscription, say so. Do not describe a trial as permanently free.

## 3. Prepare an install path someone else can follow

Test the invitation with an account that has the right server permissions, then check the onboarding steps in a test server. Explain the permissions the bot requests and why it needs them.

Give an example of a successful first action. A new administrator should know how to tell that setup worked, where to change settings and where to ask for help.

Check that the website, documentation, support invitation and privacy-policy links are current. These destinations should describe the same bot and use a consistent name.

## 4. Submit public identity details, never credentials

To [list your Discord bot on Discordium](https://discordium.org/add-bot), prepare its client ID and follow the ownership check shown in the submission flow. The current process uses a one-time code in the application's description. A bot token is not part of that proof.

Keep the client ID and bot token distinct: the ID identifies an application, while the token is a credential. Do not put credentials in listing text, screenshots, support messages or repository files.

Review the [Discordium community guidelines](https://discordium.org/guidelines) before submitting. Free submission and optional Premium visibility are separate choices; neither should be described as a guarantee of installs.

## 5. Use a listing worksheet

Copy this worksheet into your own notes and fill it with current information:

| Field | What to write |
| --- | --- |
| Main task | One clear sentence about the problem the bot solves |
| Intended users | The community or administrator who benefits |
| Working features | Three or four capabilities available now |
| Commands | Slash, prefix or both, plus one starting command |
| Pricing | Free features, meaningful limits and optional paid extras |
| Setup | Installation link, required permissions and first action |
| Help | Documentation and a working support destination |
| Privacy | Where users can read how their data is handled |

Ask someone unfamiliar with the project to read the result. If they cannot explain what the bot does or how to start, revise the listing before adding more features or promotional language.

## 6. Maintain the listing after launch

Recheck the description whenever command names, pricing or setup steps change. Remove broken support links and distinguish current functionality from future plans.

For developers connecting a listing to their bot, the [Discordium Developer API documentation](https://discordium.org/developers) covers statistics reporting, vote checks and vote webhooks. Use the documented scopes for the integration you need, and keep API tokens on the server rather than in public code or browser-side files.

A directory entry helps someone discover a project. Accurate documentation and a working first session help them decide whether to keep using it.
