# Kenji Vet Services — Deployment Guide

## Project Structure
```
kenji-vet/
├── index.html                        ← The website
├── netlify.toml                      ← Netlify config
├── netlify/
│   └── functions/
│       └── symptom-check.js          ← Secure AI function (hides API key)
└── README.md
```

---

## Step 1 — Push to GitHub

1. Go to github.com → New Repository → name it `kenji-vet`
2. Open your terminal and run:

```bash
cd kenji-vet
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/kenji-vet.git
git push -u origin main
```

---

## Step 2 — Deploy on Netlify

1. Go to netlify.com → Sign up / Log in
2. Click **"Add new site"** → **"Import an existing project"**
3. Connect GitHub → select your `kenji-vet` repo
4. Build settings: leave everything blank (no build command needed)
5. Click **Deploy site**

Your site will be live at something like: `https://kenji-vet-services.netlify.app`

---

## Step 3 — Add your Anthropic API Key (for AI Symptom Checker)

1. In Netlify dashboard → your site → **Site configuration** → **Environment variables**
2. Click **Add a variable**:
   - Key: `ANTHROPIC_API_KEY`
   - Value: your Anthropic API key (from console.anthropic.com)
3. Save → **Trigger redeploy**

✅ The AI symptom checker will now work securely — your API key is never exposed!

---

## Step 4 — Add EmailJS (for contact form emails)

1. Sign up at emailjs.com
2. Add Email Service → connect Kenji's Gmail
3. Create Email Template with variables: `{{from_name}}`, `{{reply_to}}`, `{{subject}}`, `{{message}}`
4. Get your: Service ID, Template ID, Public Key
5. Open `index.html` and replace these 3 lines near the top:

```js
const EMAILJS_PUBLIC_KEY  = 'YOUR_PUBLIC_KEY';   // ← replace
const EMAILJS_SERVICE_ID  = 'YOUR_SERVICE_ID';   // ← replace
const EMAILJS_TEMPLATE_ID = 'YOUR_TEMPLATE_ID';  // ← replace
```

6. Save → push to GitHub → Netlify auto-redeploys

---

## Step 5 — Custom Domain (optional)

1. Buy domain from Namecheap (~$10/yr for .com) or Truehost Kenya (~KSh 1,500/yr for .co.ke)
2. In Netlify → **Domain management** → **Add custom domain**
3. Follow Netlify's DNS instructions
4. Done — site live at kenjivetservices.com 🎉

---

## After Deployment Checklist
- [ ] AI symptom checker works
- [ ] Contact form sends email to Kenji
- [ ] Booking form sends email to Kenji
- [ ] Site loads on mobile
- [ ] Custom domain connected
