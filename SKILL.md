# Google Auth Agent Skill

## Description

Bootstrap AI agent identity across web services using Google OAuth sign-in. Starting from a single Google Workspace account, create and manage authenticated accounts on supported platforms.

## Capabilities

- Sign up for services using "Sign in with Google"
- Handle 2FA setup and store TOTP secrets
- Maintain account registry
- Document which services work vs. blocked

## Prerequisites

- Google Workspace account with browser session authenticated
- Browser automation capability (Playwright via Clawdbot)
- Secure secrets storage at `~/.clawdbot/secrets/`

## Commands

### Create Account on Service

```
Create an account on [SERVICE] using Google sign-in
```

The skill will:
1. Navigate to service signup/login page
2. Find and click "Sign in with Google" button
3. Complete OAuth flow (may require TOTP from stored Google secret)
4. Handle any additional signup steps
5. Set up 2FA if offered (store TOTP secret)
6. Record account details in registry

### List Accounts

```
List all accounts created via Google Auth Agent
```

Returns contents of `accounts.json` registry.

### Check Service Compatibility

```
Can you sign up for [SERVICE] with Google?
```

Checks known compatibility list and attempts discovery if unknown.

## Account Registry Format

`accounts.json`:
```json
{
  "accounts": [
    {
      "service": "github",
      "username": "jaredtribe",
      "email": "jared@tribecode.ai",
      "created": "2026-02-16T02:44:00Z",
      "auth_method": "google_oauth",
      "has_2fa": true,
      "totp_secret_path": "~/.clawdbot/secrets/github-totp.json",
      "status": "active",
      "notes": "Primary code hosting"
    }
  ]
}
```

## Security

- All credentials stored in `~/.clawdbot/secrets/` with 600 permissions
- Account creation requires owner approval
- Each account traces to the Google Workspace identity anchor
- Transparent about AI authorship where possible

## Limitations

- Services with CAPTCHA may block automated signup
- Some services detect headless browsers
- Rate limits may apply
- ToS of target services should be reviewed

## References

- [Bootstrap Report](/home/ubuntu/clawd/memory/bootstrap-report.md)
- [TOOLS.md](/home/ubuntu/clawd/TOOLS.md)
