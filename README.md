[README.md](https://github.com/user-attachments/files/26839434/README.md)
# Zynthari Gallery — Complete Setup Guide

## Admin credentials
Email:    admin@zynthari.art
Password: Admin@1234

---

## STEP 1 — Create free database at JSONBin.io (5 minutes)

1. Go to https://jsonbin.io → Sign Up (free, no credit card needed)
2. After logging in, click "API Keys" in top menu
3. Copy your **X-Master-Key** — you'll need it later
4. Click "+ Create Bin"
   - Paste: []
   - Name: zyn-users
   - Click Save
   - Copy the Bin ID from the URL bar (looks like: 64abc123def456...)
5. Create another bin:
   - Paste: []
   - Name: zyn-artworks
   - Save → copy Bin ID
6. Create another bin:
   - Paste: []
   - Name: zyn-transactions
   - Save → copy Bin ID

---

## STEP 2 — Seed the admin account

In JSONBin, open your zyn-users bin, click the Edit button, and replace [] with this exact JSON:

[
  {
    "id": "admin-001",
    "name": "Gallery Admin",
    "email": "admin@zynthari.art",
    "pwHash": "H61fe854d",
    "role": "admin",
    "token": "ZYN-ADMIN001",
    "paymentMethods": {},
    "created": "2025-01-01T00:00:00.000Z"
  }
]

Click Save. Admin login: admin@zynthari.art / Admin@1234

---

## STEP 3 — Push to GitHub

Create a new GitHub repo (e.g. zynthari-gallery), keep it Public.
Upload ALL files keeping this exact folder structure:

  netlify.toml
  package.json
  README.md
  public/
    index.html
  netlify/
    functions/
      db.js
      login.js
      register.js
      session.js
      artworks.js
      artwork-delete.js
      purchase.js
      dashboard.js
      admin.js

---

## STEP 4 — Deploy on Netlify

1. Go to https://netlify.com
2. Click "Add new site" → "Import an existing project" → "Deploy with GitHub"
3. Connect your GitHub account and select the repo
4. Leave build settings blank (netlify.toml handles everything)
5. Click "Deploy site"

---

## STEP 5 — Add environment variables (CRITICAL — site won't work without these)

In Netlify dashboard:
→ Site configuration → Environment variables → Add variable

Add ALL FIVE of these:

  Key: JSONBIN_MASTER_KEY      Value: (your master key from Step 1)
  Key: JSONBIN_USERS_BIN       Value: (your zyn-users bin ID)
  Key: JSONBIN_ARTWORKS_BIN    Value: (your zyn-artworks bin ID)
  Key: JSONBIN_TRANSACTIONS_BIN  Value: (your zyn-transactions bin ID)
  Key: SESSION_SECRET          Value: zynthari-super-secret-key-2025-xyz

After adding all 5 vars:
→ Go to Deploys → Trigger deploy → Deploy site

---

## Done! Everything works:

- Users can register → accounts saved to database permanently
- Artists can upload artwork → stays in database until deleted
- Admin panel: admin@zynthari.art / Admin@1234
- Buyer/Seller dashboards load real data
- Payment methods save to database

## To get more traffic to your site:

1. Share the URL on WhatsApp, Instagram, Twitter, TikTok
2. Post in art Facebook groups
3. Message artists directly to list their work
4. Post on Reddit: r/Art, r/DigitalArt, r/artbusiness
5. Every artwork page has share buttons — encourage artists to use them
