# rkchhabda — Multi-Domain Setup

This repo contains the starter site for **rkchhabda.github.io** and scripts/guides for securing `rkchhabda.eu.org` and `rkchhabda.duckdns.org`.

---

## 🚀 Quick Start: GitHub Pages (Instant)

```bash
# 1. Create GitHub repo named exactly: rkchhabda.github.io
# 2. Push this folder contents:
cd rkchhabda.github.io
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/rkchhabda/rkchhabda.github.io.git
git push -u origin main
```

3. **Enable Pages**: Settings → Pages → Source: "GitHub Actions"
4. **Live at**: `https://rkchhabda.github.io` (2–3 min after push)

---

## 🌍 Domain Status

| Domain | Status | DNS Control | SSL | Notes |
|--------|--------|-------------|-----|-------|
| `rkchhabda.github.io` | ✅ Ready | GitHub | Auto | Push to deploy |
| `rkchhabda.eu.org` | ⏳ Apply | Full (NS) | Cloudflare | **Apply at eu.org/arf/** |
| `rkchhabda.duckdns.org` | 🔄 Setup | A/AAAA/TXT only | Let's Encrypt | Run `Update-DuckDNS.ps1` |
| `rkchhabda.pages.dev` | 🔄 Setup | Cloudflare | Auto | Connect repo in Cloudflare Pages |

---

## 📋 EU.org Application (Do This First — Takes Weeks)

**File**: [`EU-ORG-APPLICATION-GUIDE.md`](EU-ORG-APPLICATION-GUIDE.md)

1. Go to **https://eu.org/arf/**
2. Fill form with:
   - Domain: `rkchhabda.eu.org`
   - Your real email
   - Purpose: Use template in guide
3. Submit → Wait 3 days – 4 weeks
4. On approval: Add Cloudflare nameservers via reply email

---

## 🦆 DuckDNS Setup (Instant Backup)

**File**: [`Update-DuckDNS.ps1`](../Update-DuckDNS.ps1)

1. Login at **https://www.duckdns.org** (GitHub/Reddit/Twitter/Persona)
2. Add domain: `rkchhabda` → gets token
3. Edit `Update-DuckDNS.ps1`: Replace `YOUR_TOKEN_HERE`
4. Test: `powershell -File Update-DuckDNS.ps1`
5. **Task Scheduler**: Run every 5 min, highest privileges
   - Trigger: Daily, repeat every 5 min indefinitely
   - Action: `powershell.exe -File "C:\full\path\Update-DuckDNS.ps1"`

---

## ☁️ Cloudflare Pages (Modern Alternative)

1. Go to **https://dash.cloudflare.com** → Pages
2. "Connect to Git" → Select `rkchhabda/rkchhabda.github.io`
3. Build: `Framework: None`, `Output: /` (root)
4. Live at `rkchhabda.pages.dev` instantly
5. Later: Add custom domain `rkchhabda.eu.org` in Pages → Custom domains

---

## 📁 File Structure

```
rkchhabda.github.io/
├── index.html          # Starter site
├── CNAME               # Custom domain (rkchhabda.eu.org)
├── .github/workflows/
│   └── deploy.yml      # Auto-deploy on push
├── EU-ORG-APPLICATION-GUIDE.md
└── Update-DuckDNS.ps1  # DuckDNS updater (one level up)
```

---

## 🔧 Custom Domain Priority (After EU.org Approval)

| Target | CNAME / A Record |
|--------|------------------|
| GitHub Pages | CNAME `@` → `rkchhabda.github.io` |
| Cloudflare Pages | CNAME `@` → `rkchhabda.pages.dev` |
| Render | CNAME `@` → `rkchhabda.onrender.com` |
| Home server | A `@` → your IP (via DuckDNS updater) |

**In Cloudflare DNS**: Add CNAME `@` → target, **Proxy status: Proxied** (orange cloud)

---

## ✅ Checklist

- [ ] Push `rkchhabda.github.io` repo → GitHub Pages live
- [ ] Submit EU.org application (use guide)
- [ ] Claim DuckDNS domain + set up Task Scheduler
- [ ] Connect repo to Cloudflare Pages
- [ ] When EU.org approves: Add NS to Cloudflare, enable proxy
- [ ] Add custom domains in GitHub Pages / Cloudflare Pages settings

---

## 📞 Need Help?

- EU.org mailing list: `subscribe freedns-users` → `majordomo@lists.EU.org`
- DuckDNS FAQ: https://www.duckdns.org/faqs.jsp
- GitHub Pages docs: https://docs.github.com/pages
- Cloudflare Pages docs: https://developers.cloudflare.com/pages