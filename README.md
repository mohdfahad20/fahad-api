# Fahad Portfolio — Setup Guide

## Project Structure
```
fahad-portfolio/
├── pages/
│   ├── index.js          ← serves your portfolio HTML
│   └── api/
│       └── ask.js        ← Groq API route (key stays here, server-side only)
├── public/
│   ├── index.html        ← your portfolio HTML (copy from portfolio.html)
│   └── MohdFahad_DS_Resume.pdf   ← drop your PDF here
├── .env.local            ← your Groq key (NEVER commit this)
├── .gitignore            ← already ignores .env.local
├── next.config.js
└── package.json
```

---

## LOCAL DEVELOPMENT

### Step 1 — Install dependencies
```bash
cd fahad-portfolio
npm install
```

### Step 2 — Add your Groq key to .env.local
Open `.env.local` and replace the placeholder:
```
GROQ_API_KEY=gsk_your_actual_key_here
```
Get a free key at: https://console.groq.com → API Keys

### Step 3 — Add your resume PDF
Copy your resume PDF into the `public/` folder:
```
public/MohdFahad_DS_Resume.pdf
```

### Step 4 — Run locally
```bash
npm run dev
```
Open http://localhost:3000

### Step 5 — Test AI mode
- Open the terminal (⌗ terminal button)
- Switch to ✦ AI mode
- Ask: "What projects has Fahad built?"
- It should respond using Groq — key never visible in browser

---

## DEPLOYMENT TO VERCEL

### Step 1 — Push to GitHub
```bash
git init
git add .
git commit -m "initial portfolio"
```
Create a new repo on github.com (do NOT add README, .gitignore — you already have them)
```bash
git remote add origin https://github.com/YOUR_USERNAME/fahad-portfolio.git
git branch -M main
git push -u origin main
```

### Step 2 — Connect to Vercel
1. Go to https://vercel.com
2. Sign up / log in with GitHub
3. Click "Add New Project"
4. Import your `fahad-portfolio` repo
5. Leave all settings as default (Vercel auto-detects Next.js)
6. Click Deploy — but DON'T visit yet

### Step 3 — Add your Groq key to Vercel
1. In your Vercel project → Settings → Environment Variables
2. Add:
   - Name: `GROQ_API_KEY`
   - Value: `gsk_your_actual_key_here`
   - Environments: ✓ Production ✓ Preview ✓ Development
3. Click Save

### Step 4 — Redeploy
Go to Deployments tab → click the three dots on latest → Redeploy
(This makes Vercel pick up the new env variable)

### Step 5 — Done
Your portfolio is live at `https://fahad-portfolio.vercel.app`
Or add a custom domain in Vercel → Settings → Domains

---

## HOW THE KEY STAYS SAFE
- `.env.local` → only on your computer, gitignored
- Vercel env var → only on Vercel's servers, never sent to browser
- `pages/api/ask.js` → runs on server, reads `process.env.GROQ_API_KEY`
- Your HTML calls `/api/ask` → server adds the key → calls Groq
- Browser only ever sees the response, never the key

## FORMSPREE (Contact Form)
1. Go to https://formspree.io → Sign up free
2. Create a new form → copy the Form ID (e.g. `xpwzgkja`)
3. In `public/index.html`, find `YOUR_FORMSPREE_ID` and replace it
4. Push to GitHub → Vercel auto-redeploys
