# Setting up the CMS (Decap) — one-time guide

Your site now reads all its content from the four files in `content/`:

| File | What it holds |
|------|----------------|
| `content/articles.json` | Essays & field notes |
| `content/maxims.json` | One-line maxims |
| `content/notes.json` | Leadership notes |
| `content/frameworks.json` | Infographic frameworks |

You can edit those JSON files by hand any time. **Decap CMS** gives you a friendly
admin screen (`/admin`) so you don't have to — you get title fields, a publish
button, drafts, and image uploads, and it saves changes straight back to your repo.

Decap is git-based, so it needs the site in a Git repo and hosted somewhere that
can authenticate you. The easiest free path is **GitHub + Netlify**. ~20 minutes,
once.

---

## Step 1 — Put the project on GitHub
1. Create a new repository at https://github.com/new (private is fine).
2. Upload this whole project to it (the `Nicholas You.dc.html`, `content/`,
   `admin/`, `assets/`, etc.). If you use the GitHub website, drag the files in;
   if you use git on your computer, `git init && git add . && git commit && git push`.

## Step 2 — Deploy to Netlify (free)
1. Sign up at https://app.netlify.com using your GitHub account.
2. **Add new site → Import an existing project → GitHub → pick your repo.**
3. Build settings: leave **build command empty** and set **publish directory** to
   the repo root (just `/` or `.`). This is a static site — no build step.
4. Deploy. Netlify gives you a URL like `https://yourname.netlify.app`
   (you can point `nicholasyou.com` at it later under Domain settings).

## Step 3 — Turn on logins (Netlify Identity + Git Gateway)
1. In your Netlify site: **Integrations / Identity → Enable Identity.**
2. Under **Identity → Registration**, set it to **Invite only** (so randoms can't sign up).
3. Under **Identity → Services → Git Gateway → Enable Git Gateway.**
   This is what lets the admin panel write to your repo.
4. **Identity → Invite users → invite your own email.** Check your inbox, accept,
   and set a password.

## Step 4 — Log in and edit
1. Go to `https://your-site/admin/` (note the trailing slash).
2. Log in with the email/password from Step 3.
3. You'll see **Articles, Maxims, Leadership Notes, Frameworks.** Edit, then
   **Publish** — Decap commits to your repo, Netlify redeploys in ~30s, and the
   change is live. No tokens, no me.

---

## Notes & gotchas
- **Default branch:** `admin/config.yml` assumes your branch is `main`. If GitHub
  made yours `master`, change the `branch:` line in that file.
- **URL slugs:** the `id` field on articles/notes/frameworks is the permanent link
  (e.g. `/#/article/governing-the-machine`). Set it once; changing it later breaks
  old links.
- **Featured posts:** toggle "Featured on homepage" on an article to surface it on
  the home page (up to 6 show, newest first).
- **Frameworks layout:** pick `rows` (numbered list) and fill the **Rows** list, OR
  pick `stats` (big-number grid) and fill the **Stats** list.
- **Credentials** on the About page are still in the HTML file (they rarely change).
  If you want those in the CMS too, say the word and I'll add a collection.

## Alternative: skip Netlify, use the GitHub backend directly
If you'd rather not use Netlify Identity, Decap can talk to GitHub via an OAuth app
you host. It's more fiddly (you run a tiny OAuth proxy). The Netlify path above is
the recommended one — only go here if you have a reason to.
