# ZeroHost Minecraft Server Template

GitHub Actions template for on-demand Minecraft servers with Discord control, playit.gg tunneling, and Google Drive world backups.

**Do not set up manually** — use the [ZeroHost desktop wizard](https://hollenite.space/#download) to automate all configuration.

## What the wizard configures

### GitHub Actions secrets

| Secret | Description |
|--------|-------------|
| `DISCORD_BOT_TOKEN` | Discord bot token |
| `DISCORD_CHANNEL_ID` | Channel for server notifications |
| `GH_PAT` | GitHub PAT with `repo` and `actions:write` scopes |
| `PLAYIT_SECRET` | playit.gg agent secret key |
| `GDRIVE_SERVICE_ACCOUNT_JSON` | Google service account JSON |
| `GDRIVE_FOLDER_ID` | Google Drive folder ID for world backups |
| `RCON_PASSWORD` | Auto-generated RCON password |

### Repository variables

| Variable | Description | Default |
|----------|-------------|---------|
| `PLAYIT_ADDRESS` | Public playit.gg tunnel address | Set by wizard after claim |
| `MAX_PLAYERS` | Max players | `10` |
| `PAPER_VERSION` | Paper MC version | `1.21.11` |
| `PAPER_BUILD` | Paper build number | `69` |

## How it works

1. User types `/start` in Discord
2. Bot triggers the `minecraft.yml` workflow via GitHub Actions API
3. Runner downloads Paper, loads world from Google Drive, starts playit tunnel
4. Monitor script tracks players, forwards events to Discord, auto-saves and shuts down when empty
5. User types `/stop` to cancel the workflow (triggers world save)

## Discord bot (Personal tier)

The ZeroHost wizard deploys `bot/bot.py` locally on the buyer's machine. Required environment variables:

```
DISCORD_BOT_TOKEN
GH_PAT
GITHUB_REPO
DISCORD_GUILD_ID
DISCORD_CHANNEL_ID
PLAYIT_ADDRESS
```

## Template usage

The ZeroHost wizard bundles this directory into the desktop installer and pushes it to a new **public** repository on the buyer's GitHub account via the Git Data API. No external template repository is required.
