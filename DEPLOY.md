# Deploying zhandayeva.com

The folder is already a git repo with everything committed on `main`. Three things to do:

## 1. Create the GitHub repo

In a browser, go to: **https://github.com/new**

- **Repository name:** `zhandayeva-website`
- **Visibility:** Public (required for free GitHub Pages)
- Leave everything else empty (no README, no .gitignore, no license — we already have them)
- Click **Create repository**

GitHub will then show you a page with setup commands. Ignore those — use the ones below instead.

## 2. Push from your terminal

Open Terminal and paste these one at a time. Replace `YOUR-USERNAME` with your actual GitHub username on the first line:

```bash
cd "/Users/raushanzhandayeva/Library/Application Support/Claude/local-agent-mode-sessions/ab821941-51c0-4e14-8cd8-ed8557f04a2d/6295bfdc-b7d5-4f58-8a07-ba87c65fc109/local_c25da7aa-4551-485e-91e0-9aec69617734/outputs"

git remote add origin https://github.com/YOUR-USERNAME/zhandayeva-website.git
git push -u origin main
```

If git asks for credentials, use a **personal access token** (not your password). If you don't have one, GitHub's docs walk you through it — or use the GitHub CLI: `brew install gh && gh auth login`.

## 3. Turn on Pages and the custom domain

Once pushed, go to your repo's **Settings → Pages**:

- **Source:** Deploy from a branch
- **Branch:** `main` / `/ (root)` → **Save**
- **Custom domain:** `zhandayeva.com` → **Save**
- Wait a few minutes, then check **Enforce HTTPS**

## 4. Point DNS at Wix to GitHub

Sign in to Wix, find the DNS settings for `zhandayeva.com` (Domains → Advanced → Edit DNS), and replace the existing records with:

**A records (apex `@`):**
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**CNAME record (`www`):**
```
YOUR-USERNAME.github.io
```

If Wix is also where the domain is registered: keep the registrar there but change the DNS A/CNAME records as above. Don't delete the domain. **Note:** if you use Wix's email service tied to this domain, leave any MX records alone.

DNS can take 10 minutes to a few hours. Once it propagates, https://zhandayeva.com loads your new site.

## Future updates

Anytime you want to push changes:
```bash
cd "/Users/raushanzhandayeva/Library/Application Support/Claude/local-agent-mode-sessions/ab821941-51c0-4e14-8cd8-ed8557f04a2d/6295bfdc-b7d5-4f58-8a07-ba87c65fc109/local_c25da7aa-4551-485e-91e0-9aec69617734/outputs"
git add .
git commit -m "describe what changed"
git push
```

GitHub rebuilds automatically.
