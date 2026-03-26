# CallSignal — Sales Intelligence Dashboard

## What's in this folder

```
index.html         ← The entire app (open this in a browser to test locally)
api/
  gong-proxy.js    ← Serverless proxy for Gong API (required for Vercel)
vercel.json        ← Vercel routing config
README.md          ← This file
```

---

## Deploy to Vercel (5 minutes)

### Option A — Drag & Drop (easiest, no account needed)
1. Go to **vercel.com**
2. Click **"Start Deploying"** — no sign-up required for basic use
3. Drag this entire folder onto the page
4. Vercel gives you a live URL like `callsignal-abc123.vercel.app`
5. Share that URL with your team

### Option B — GitHub (best for ongoing updates)
1. Create a free GitHub account at github.com
2. Create a new repository, upload these files
3. Go to vercel.com → Import from GitHub
4. Select your repo → Deploy
5. Any time you update the files in GitHub, Vercel auto-redeploys

---

## Getting your API keys

### Gong Access Key + Secret
1. Log into Gong as a **Technical Admin**
2. Go to: **Settings → Company Settings → API**
3. Click **"Create"** to generate an Access Key + Secret
4. Copy both — you only see the secret once

### Anthropic API Key
1. Go to **platform.anthropic.com**
2. Create an account (separate from Claude.ai)
3. Go to **API Keys → Create Key**
4. Copy the key (starts with `sk-ant-api...`)
5. Add a credit card — you'll be charged ~$0.01–0.03 per transcript analyzed
6. **Tip:** Set a monthly spending limit under Billing settings so there are no surprises

---

## First-time setup in the app

1. Open the app URL
2. Paste your **Gong Access Key + Secret** and **Anthropic API Key**
3. Click **"Save & Continue"**
4. Go to **Account List** tab → Upload your CRM export CSV
5. Click **"Sync from Gong"** — the app will only pull calls matching companies in your CSV
6. Wait for analysis to complete (about 5–10 seconds per call)

---

## CSV format for account list

Export from Salesforce, HubSpot, or any CRM. The app reads these columns:

| Column | Required | Notes |
|--------|----------|-------|
| `Account Name` | ✅ Yes | Used to match Gong calls |
| `Opportunity Owner` | No | Rep name |
| `Amount` | No | ACV — used for tagging |
| `Industry` | No | Used for filtering |
| `Number of Employees` | No | Used for filtering |
| `Lead Source` | No | Used for filtering |
| `Stage` | No | Used for filtering |

---

## How Gong matching works

When you sync, the app:
1. Pulls all calls from the last 180 days in Gong
2. Checks each call's external participants against your account list
3. Only downloads transcripts for matched accounts
4. Sends each transcript to Claude for scoring
5. Adds scored calls to your dashboard

**Tip:** The matching is fuzzy — "Armitage Heating" will match "Armitage Heating and Cooling". But the closer your CRM names match how they appear in Gong, the better.

---

## Cost estimate

For a team with 20 reps doing 5 calls/day:
- 100 calls/day × $0.02 avg = **~$2/day**
- Monthly: **~$60/month** for full team coverage

For most teams with 10–50 calls/week: **under $5/month total**.
