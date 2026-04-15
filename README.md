[README.md](https://github.com/user-attachments/files/26755090/README.md)
# Zynthari Gallery — Setup Guide

## What's in this folder
- `public/index.html` — the full website frontend
- `netlify/functions/` — the backend API (runs on Netlify serverless)
- `netlify.toml` — tells Netlify how to build and route
- `package.json` — installs node-fetch for the functions

## STEP 1 — Create your free database (JSONBin.io)

1. Go to https://jsonbin.io and click **Sign Up** (free, no credit card)
2. After login, click **API Keys** in the top menu → copy your **Master Key**
3. Click **Create Bin** → paste `[]` → Name it `zyn-users` → Save → copy the **Bin ID** from the URL
4. Create another bin → paste `[]` → Name it `zyn-artworks` → Save → copy the Bin ID
5. Create another bin → paste `[]` → Name it `zyn-transactions` → Save → copy the Bin ID

## STEP 2 — Seed the admin user

In JSONBin, click your `zyn-users` bin → Edit → paste this (replace the bin content):
```json
[
  {
    "id": "admin-001",
    "name": "Gallery Admin",
    "email": "admin@zynthari.art",
    "pwHash": "H4e5f1c2a",
    "role": "admin",
    "token": "ZYN-ADMIN001",
    "paymentMethods": {},
    "created": "2025-01-01T00:00:00.000Z"
  }
]
```
**Admin login:** admin@zynthari.art / Admin@1234

## STEP 3 — Push to GitHub

1. Create a new GitHub repository (e.g. `zynthari-gallery`)
2. Upload ALL files keeping the folder structure:
   ```
   netlify.toml
   package.json
   public/index.html
   netlify/functions/db.js
   netlify/functions/session.js
   netlify/functions/login.js
   netlify/functions/register.js
   netlify/functions/artworks.js
   netlify/functions/artwork-delete.js
   netlify/functions/purchase.js
   netlify/functions/dashboard.js
   netlify/functions/admin.js
   ```

## STEP 4 — Deploy on Netlify

1. Go to https://netlify.com → **Add new site** → **Import from Git**
2. Connect GitHub, select your repo
3. Build settings: leave blank (netlify.toml handles it)
4. Click **Deploy site**

## STEP 5 — Add environment variables (CRITICAL)

In Netlify dashboard → **Site configuration** → **Environment variables** → Add these:

| Key | Value |
|-----|-------|
| `JSONBIN_MASTER_KEY` | your Master Key from Step 1 |
| `JSONBIN_USERS_BIN` | your zyn-users Bin ID |
| `JSONBIN_ARTWORKS_BIN` | your zyn-artworks Bin ID |
| `JSONBIN_TRANSACTIONS_BIN` | your zyn-transactions Bin ID |
| `SESSION_SECRET` | any long random string e.g. `zynthari-super-secret-key-2025-xkq` |

Then go to **Deploys** → **Trigger deploy** → **Deploy site**

## Done! Your site is live.

- Users can register and their accounts persist forever
- Artists can upload artwork and it stays until they delete it
- Buyers can purchase and see their collection
- Admin: admin@zynthari.art / Admin@1234
