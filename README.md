# Stable Redirect for Ticketing QR Codes

This folder is a **GitHub Pages** site that provides a **stable URL** for your ticketing QR codes.

## The Problem
- Cloudflare Quick Tunnel gives a new URL each time you restart it
- QR codes are printed on devices – you can't reprint them every time
- You need a URL that **never changes**

## The Solution
- QR codes point to **this GitHub Pages URL** (e.g. `https://YOUR_USERNAME.github.io/it-ticketing/`)
- This page redirects to your **current tunnel URL**
- When the tunnel URL changes, you only update `config.json` and push – **no need to change QR codes**

---

## Setup (One-Time)

### 1. Create a GitHub Account
If you don't have one: https://github.com/signup

### 2. Create a New Repository
1. Go to https://github.com/new
2. Repository name: `it-ticketing` (or any name)
3. Set to **Public**
4. Do **not** initialize with README
5. Click **Create repository**

### 3. Upload These Files
Push the contents of this folder to your repo:

```bash
cd "e:\ITManagement\github-redirect"
git init
git add .
git commit -m "Initial redirect page"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/it-ticketing.git
git push -u origin main
```

Or use GitHub's web interface: **Upload files** and add `index.html` and `config.json`.

### 4. Enable GitHub Pages
1. In your repo, go to **Settings** → **Pages**
2. Under **Source**, select **Deploy from a branch**
3. Branch: **main**, folder: **/ (root)**
4. Click **Save**
5. Wait 1–2 minutes. Your URL will be: `https://YOUR_USERNAME.github.io/it-ticketing/`

### 5. Update Your Main App
In `Frontend\.env`:
```
VITE_TICKETING_URL=https://YOUR_USERNAME.github.io/it-ticketing
```

Restart the Main Frontend. QR codes will now use this stable URL.

---

## When Your Tunnel URL Changes

1. Open `config.json` in this folder
2. Update the `tunnelUrl` value to your new tunnel URL
3. Push to GitHub:
   ```bash
   cd "e:\ITManagement\github-redirect"
   git add config.json
   git commit -m "Update tunnel URL"
   git push
   ```
4. Done. QR codes stay the same – they still point to GitHub, which now redirects to the new tunnel.

---

## QR Code URL Format

- Base: `https://YOUR_USERNAME.github.io/it-ticketing/`
- With device: `https://YOUR_USERNAME.github.io/it-ticketing/?d=123`
- The `?d=123` is the device Entry ID
