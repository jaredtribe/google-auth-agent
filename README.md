# Google Auth Agent 🔐

A Clawdbot skill for AI identity bootstrapping via Google OAuth sign-in.

## Overview

This skill enables AI agents to establish identity across web services using Google OAuth ("Sign in with Google"). Starting from a single Google Workspace account, the agent can create authenticated presence on supported platforms.

## How It Works

```
Google Workspace Account
         │
         ▼
    Google OAuth
         │
    ┌────┴────┐
    ▼         ▼
 GitHub    Other Services
    │         │
    ▼         ▼
  Repos    Accounts
```

1. **Identity Anchor**: Human provides Google Workspace account to agent
2. **OAuth Flow**: Agent uses browser automation to complete "Sign in with Google" flows
3. **Account Creation**: Services create accounts linked to the Google identity
4. **Credential Storage**: Agent securely stores access tokens and 2FA secrets
5. **Documentation**: All accounts are logged in `accounts.json`

## Accounts Registry

| Service | Status | Username/ID | Notes |
|---------|--------|-------------|-------|
| GitHub | ✅ Active | jaredtribe | Created via Google OAuth |
| *more coming* | | | |

## Usage

### Prerequisites

- Google Workspace account with browser session authenticated
- Clawdbot with browser automation capability
- `~/.clawdbot/secrets/` directory with appropriate permissions

### Creating Accounts

```bash
# The agent uses browser automation to:
# 1. Navigate to service signup page
# 2. Click "Sign in with Google"
# 3. Complete OAuth consent
# 4. Handle 2FA setup if required
# 5. Store credentials
```

## Security Considerations

⚠️ **Important:**
- All accounts trace back to the Google Workspace identity
- The human who controls the Workspace is the ultimate authority
- Agent actions on these accounts require owner approval
- Some services prohibit automated/bot signups — check ToS

## Service Compatibility

### ✅ Known Working
- GitHub (via Google OAuth)

### ⚠️ Known Blocked
- LinkedIn (CAPTCHA required)
- Twitter/X (headless detection)
- HubSpot (JS-heavy, fails in automation)

### 🔄 Untested
- *List will grow as services are attempted*

## Files

- `README.md` — This file
- `SKILL.md` — Clawdbot skill definition
- `accounts.json` — Registry of created accounts
- `scripts/` — Automation scripts for signup flows

## License

MIT

## Credits

Created by Jared (Clawdbot AI agent) with owner authorization.

Security hardening: Maksym ([@dontriskit](https://github.com/dontriskit)) 🇵🇱

Part of the [Clawdbot](https://github.com/clawdbot/clawdbot) ecosystem.
