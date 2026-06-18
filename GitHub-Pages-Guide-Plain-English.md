# Putting your website online with GitHub Pages — a plain-English guide

This guide takes you from "files on my computer" to "live at **https://jimdelaney.net**" without touching a command line or installing anything. You only need a web browser.

**Roughly how long:** 30–45 minutes, plus some waiting for the internet to catch up (up to an hour, occasionally longer, for the domain and the padlock to go live).

**A few words you'll see, in plain terms:**

- **Repository (or "repo")** — just a folder that lives on GitHub. Your website files go inside it.
- **GitHub Pages** — a free GitHub feature that takes the files in your repo and serves them as a real website.
- **DNS** — the internet's address book. It's what tells `jimdelaney.net` to point at your GitHub site. You'll edit this in Cloudflare.
- **HTTPS / the padlock** — the little lock icon in the browser bar. It means the connection is secure. GitHub sets this up for you for free.

**What you need before you start:**

1. The `site` folder (the one containing `index.html`, `cv.html`, `styles.css`, the `assets` folder, and a file called `CNAME`).
2. A login for **Cloudflare** (where your domain `jimdelaney.net` is managed).
3. An email address to make a free GitHub account.

> Tip: keep this guide open in one browser tab and do the work in another.

---

## Part 1 — Create a free GitHub account

If you already have a GitHub account, skip to Part 2.

1. Go to **https://github.com** and click **Sign up**.
2. Enter your email, pick a password, and choose a **username**. Your username will appear in your web address behind the scenes, so something tidy like `jimdelaney` is ideal (it doesn't have to be perfect — it won't show on your final site).
3. Verify your email when GitHub sends you a code.
4. When asked about a plan, choose the **Free** plan. It's all you need.

Write your username down — you'll use it in Part 5.

---

## Part 2 — Create the repository (the online folder)

1. Once logged in, click the **+** icon in the top-right corner of GitHub and choose **New repository**.
2. **Repository name:** type something simple, e.g. `jimdelaney-website`.
3. **Description:** optional — you can write "My consultancy website."
4. Set it to **Public**. (Free GitHub Pages requires the repo to be public. Don't worry — only your finished website is visible, and that's the point.)
5. Leave every checkbox **unticked** (no README, no .gitignore, no licence). You want an empty repo.
6. Click **Create repository**.

You'll land on a fairly empty page with some instructions. Ignore the instructions — we're going to upload files the easy way.

---

## Part 3 — Upload your website files

This is the step where your site actually goes onto GitHub.

1. On your new repository page, find the link that says **"uploading an existing file"** (it's in the grey instructions box). Click it.
   - If you don't see it, click the **Add file** button near the top and choose **Upload files**.
2. Open your `site` folder on your computer in a separate window (Finder).
3. **Select everything *inside* the `site` folder** — that means `index.html`, `cv.html`, `styles.css`, `CNAME`, and the `assets` folder. (Select the *contents*, not the `site` folder itself.)
4. **Drag them onto the GitHub upload area** in your browser. GitHub will accept the `assets` folder and keep everything organised.
   - Wait until every file shows up in the list, including the ones inside `assets`.
5. Scroll down to the **"Commit changes"** box. "Commit" just means "save." You can leave the default message ("Add files via upload").
6. Click the green **Commit changes** button.

That's your whole website, now on GitHub. ✔

> Important: make sure the file called **`CNAME`** uploaded. It's what links your site to `jimdelaney.net`. If you don't see it in the file list afterward, repeat the upload for just that file.

---

## Part 4 — Turn on GitHub Pages

1. On your repository page, click the **Settings** tab (top-right area, with a gear icon).
2. In the left-hand menu, scroll down and click **Pages**.
3. Under **"Build and deployment" → "Source,"** make sure it says **Deploy from a branch**.
4. Under **Branch**, open the first dropdown and choose **main**. Leave the folder dropdown as **/ (root)**.
5. Click **Save**.

GitHub now starts building your site. Wait about a minute, then refresh the page. You should see a message like *"Your site is live at…"* with a temporary address ending in `github.io`. Click it to check your site appears. It won't be on your own domain yet — that's the next part.

---

## Part 5 — Connect your domain (jimdelaney.net)

This has two halves: telling **Cloudflare** to point your domain at GitHub, and telling **GitHub** that your domain is yours.

### 5a. Add the DNS records in Cloudflare

1. Log in to **https://dash.cloudflare.com** and click your domain **jimdelaney.net**.
2. In the left menu, click **DNS → Records**.
3. If there are existing **A records** or **CNAME records** for `@` or `www` left over from before, delete them (click Edit → Delete). This avoids conflicts.
4. Now add the following records one at a time using the **Add record** button. For each A record: Type = **A**, Name = **@**, and paste the IP address into **IPv4 address**.

   | Type  | Name (host) | Value / points to            |
   |-------|-------------|------------------------------|
   | A     | `@`         | `185.199.108.153`            |
   | A     | `@`         | `185.199.109.153`            |
   | A     | `@`         | `185.199.110.153`            |
   | A     | `@`         | `185.199.111.153`            |
   | CNAME | `www`       | `YOUR-USERNAME.github.io`    |

   Replace **YOUR-USERNAME** with your GitHub username from Part 1 (for example `jimdelaney.github.io`). Note the dot before "github" and no `https://`.

5. **Very important:** for each of these records, click the **orange cloud** icon in the "Proxy status" column so it turns **grey** ("DNS only"). GitHub needs this while it sets up your security certificate. (You can switch it back to orange later if you want — see the note at the end.)
6. Save each record.

### 5b. Tell GitHub your domain

1. Go back to your GitHub repo → **Settings → Pages**.
2. In the **Custom domain** box, type **`jimdelaney.net`** and click **Save**.
   - GitHub may already have filled this in for you, because the `CNAME` file you uploaded does exactly this. If so, great — you can leave it.
3. GitHub will run a **DNS check**. It can take a few minutes (occasionally up to an hour) for the green tick to appear while the internet updates. A temporary warning here is normal — give it time.

---

## Part 6 — Turn on the security padlock (HTTPS)

1. **In Cloudflare:** left menu → **SSL/TLS → Overview**. Set the encryption mode to **Full**.
   - ⚠️ Do **not** choose "Flexible" — with GitHub Pages it causes the site to load endlessly and never open. **Full** is the correct choice.
2. **In GitHub:** Settings → Pages. Once it's available (it appears after the DNS check passes), tick the box **Enforce HTTPS**. This makes sure visitors always get the secure version.
   - If the box is greyed out, GitHub is still issuing your certificate. Check back in 15–60 minutes.

---

## Part 7 — Check it all works

In your browser, visit each of these and confirm your site loads with a padlock:

- **https://jimdelaney.net**
- **https://www.jimdelaney.net** (should redirect to the main one)

Click around — the menu, the CV page, the LinkedIn button, the Download PDF button — to make sure everything opens. If something looks unstyled (plain text, no colours), it usually just means a file is still updating; wait a few minutes and refresh.

🎉 That's it — your consultancy site is live.

---

## Updating your site later (the easy way)

Whenever you want to change wording, swap a photo, or tweak anything:

1. Edit the file on your computer (for example, open `index.html`).
2. Go to your GitHub repo → **Add file → Upload files**.
3. Drag the changed file(s) in, then click **Commit changes**.
4. GitHub republishes automatically within a minute or two. Refresh your site to see the change.

Uploading a file with the same name simply replaces the old one — you don't need to delete anything first.

> Even easier for small text tweaks: in GitHub, click the file (e.g. `index.html`), click the **pencil icon** to edit it right in the browser, make your change, and click **Commit changes**. No downloading or re-uploading at all.

---

## If something goes wrong — common fixes

- **"There isn't a GitHub Pages site here" / 404.** Give it a few minutes after Part 4. Double-check Settings → Pages shows branch **main** and folder **/ (root)**, and that `index.html` is at the *top level* of the repo (not inside a `site` folder).
- **Site loads as plain text with no styling.** The `styles.css` file or the `assets` folder didn't upload, or `index.html` is in a subfolder. Re-check that all files sit at the top level of the repo alongside `index.html`.
- **The page keeps reloading and never opens.** Cloudflare's SSL mode is set to "Flexible." Change it to **Full** (Part 6).
- **Domain still shows the old/blank page after an hour.** Confirm the four A records and the `www` CNAME are exactly as in the table, and that their proxy clouds are **grey** ("DNS only").
- **"Enforce HTTPS" is greyed out.** The certificate is still being created. Wait 15–60 minutes and refresh the Pages settings.
- **Logo or photos missing.** Confirm the `assets` folder uploaded with its files inside it.

---

## One optional extra (do this later, if you like)

Once everything works and the padlock is solid, you can go back to Cloudflare → DNS and switch the proxy clouds from grey back to **orange** on the A records. This puts Cloudflare's speed and protection in front of your site. If you do, make sure SSL/TLS stays on **Full**. If anything misbehaves after switching, just turn them grey again — it's completely reversible.

---

*Questions while you're doing this? Tell me which step and what you're seeing on screen, and I'll walk you through it.*
