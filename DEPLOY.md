# Deploying jimdelaney.net to GitHub Pages

Your site lives in this folder: `index.html`, `styles.css`, and `CNAME`.
The `CNAME` file tells GitHub Pages to serve the site at `jimdelaney.net` — leave it in place.

## 1. Put the code on GitHub

Create a new repository on GitHub (e.g. `jimdelaney-site`), then from this folder:

```bash
git init
git add .
git commit -m "Initial site"
git branch -M main
git remote add origin https://github.com/<your-username>/jimdelaney-site.git
git push -u origin main
```

## 2. Turn on GitHub Pages

In the repo: **Settings → Pages**.

- **Source:** Deploy from a branch
- **Branch:** `main`, folder `/ (root)`
- Click **Save**.

After a minute the **Custom domain** box should show `jimdelaney.net` (read from the `CNAME` file). If not, type it in and Save.

## 3. DNS in Cloudflare

In the Cloudflare dashboard for `jimdelaney.net`, open **DNS → Records** and add:

| Type  | Name  | Value                  |
|-------|-------|------------------------|
| A     | @     | 185.199.108.153        |
| A     | @     | 185.199.109.153        |
| A     | @     | 185.199.110.153        |
| A     | @     | 185.199.111.153        |
| CNAME | www   | <your-username>.github.io |

Set **Proxy status** to **DNS only** (grey cloud), not proxied, while GitHub
provisions the certificate. You can switch it back to proxied later if you want
Cloudflare's CDN in front.

## 4. SSL/TLS setting (important)

In Cloudflare: **SSL/TLS → Overview**, set the mode to **Full**.
Do *not* use **Flexible** — it causes an infinite redirect loop with GitHub Pages.

## 5. Finish

Back in **Settings → Pages**, tick **Enforce HTTPS** once it becomes available
(can take a few minutes to an hour for the cert to issue).

Done — `https://jimdelaney.net` will serve this site, and every `git push` to
`main` republishes it automatically.

## Files in this site

- `index.html` — the main one-page site (About, Practice, What I do, How I work, Contact)
- `cv.html` — your full CV, with a button to download the PDF
- `styles.css` — all styling (colors, spacing, fonts)
- `assets/headshot.jpg` — the portrait shown in the hero
- `assets/James-Delaney-CV-2026.pdf` — the downloadable CV
- `CNAME` — binds the site to `jimdelaney.net`

## Your headshot

`assets/headshot.jpg` is your photo, cleaned up: recomposed, upscaled, denoised and
sharpened, with the busy park background softened to push focus onto your face, plus
a gentle warm grade and vignette. To swap in a different photo later, just save it
over that file with the same name (square images work best).

## Editing the site

Edit `index.html` / `cv.html` (content) and `styles.css` (look), then:

```bash
git add .
git commit -m "Update content"
git push
```
