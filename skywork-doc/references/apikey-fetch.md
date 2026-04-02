# Skywork API Key Setup Guide (OpenClaw)

## SKYWORK_API_KEY Not Configured

When the `SKYWORK_API_KEY` environment variable is not set, follow these steps:

### 1. Get API Key

Visit the Skywork website and sign in to your account:

**https://skywork.ai**

- Log in with your Skywork account
- Open account / Settings / API Key (**https://skywork.ai/?openApiKeySetting=1**)
- Create or copy your **API key**

If your organization uses a separate console or test environment, use the URL and credentials your team provides.

### 2. Configure OpenClaw

Edit the OpenClaw configuration file: `~/.openclaw/openclaw.json`

In current OpenClaw, Skywork skills store the key under `skills.entries.<Skill Name>.apiKey` (not under `env`).
OpenClaw will inject this value into the skill's `SKYWORK_API_KEY` environment when `primaryEnv` matches.
Add or merge the following structure (adjust the skill name to match the installed skill):

```json
{
  "skills": {
    "entries": {
      "Skywork Document": {
        "enabled": true,
        "apiKey": "your_actual_skywork_api_key_here"
      }
    }
  }
}
```

Replace `"your_actual_skywork_api_key_here"` with your real key.

For multiple Skywork skills, repeat the same `apiKey` field on each skill entry.

### 3. Verify Configuration

```bash
# Check JSON format
cat ~/.openclaw/openclaw.json | python3 -m json.tool
```

### 4. Restart OpenClaw

```bash
openclaw gateway restart
```

## Troubleshooting

- Ensure `~/.openclaw/openclaw.json` exists and is valid JSON
- Confirm the API key is active and not expired
- Check Skywork account status, membership, or quota if requests fail with auth or benefit errors
- Restart OpenClaw after configuration changes

**Recommended**: Use the OpenClaw configuration file for centralized environment management.
