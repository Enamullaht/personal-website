# Enamullah T. — Engineering Portfolio Website

A single-page, self-contained portfolio site. No build step, no framework,
no dependencies to install — it's plain HTML/CSS/JS plus a folder of assets.

## Folder structure

```
project-name/
│
├── index.html                  ← the entire site (HTML + CSS + JS, all inline)
├── robots.txt                  ← tells search engines what to crawl
├── sitemap.xml                 ← tells search engines what pages exist
├── README.md                   ← this file
└── assets/
    ├── enam1.jpg                                  ← homepage portrait
    ├── enam2.jpg                                  ← "Meet the Engineer" portrait
    ├── favicon.svg                                ← browser tab icon
    ├── LinkedIn_Resume_Enamullah_T.pdf             ← recruiter download
    ├── Engineering_Portfolio_Enamullah_T.pdf       ← recruiter download
    └── Executive_Achievements_Enamullah_T.pdf      ← recruiter download
```

Nothing else is required. Fonts (Space Grotesk, IBM Plex Sans, IBM Plex Mono)
load from Google Fonts over the internet — no local font files needed, but
the browser does need an internet connection to fetch them.

## Deploying

The one rule for all three platforms: **keep `index.html` and the `assets/`
folder in the same directory, at the root of what you deploy.** Don't nest
them inside another folder or separate them.

### GitHub Pages
1. Create a new repository (or use an existing one).
2. Upload `index.html`, `robots.txt`, `sitemap.xml`, and the `assets/` folder
   to the repository root (drag-and-drop works on github.com, or `git add` +
   `git push` from your machine).
3. Go to **Settings → Pages**, set **Source** to your main branch and `/`
   (root) folder, then save.
4. GitHub gives you a URL like `https://yourusername.github.io/repo-name/`.
   Your site is live within a minute or two.

### Vercel
1. Go to vercel.com, click **Add New → Project**.
2. Either connect the GitHub repo above, or drag the whole project folder
   into Vercel's "Import" screen if you're not using Git.
3. Framework preset: choose **Other** (it's a static site, no build command
   needed).
4. Deploy. Vercel gives you a `.vercel.app` URL immediately, and you can
   attach a custom domain from the project settings.

### Netlify
1. Go to netlify.com, click **Add new site → Deploy manually**.
2. Drag the project folder (containing `index.html` and `assets/`) directly
   onto the upload area — no Git needed for this method.
3. Netlify deploys it instantly and gives you a `.netlify.app` URL.
4. (Optional) For automatic redeploys on every change, connect it to a
   GitHub repo instead via **Add new site → Import from Git**.

## Before you go live: update these

**Your domain.** Search the file for `your-domain.com` — it appears in
`index.html` (canonical link, Open Graph tags), `robots.txt`, and
`sitemap.xml`. Replace every instance with your real deployed URL once you
know it.

**Your Web3Forms access key.** The contact form and the recruiter
document-unlock form both send submissions through
[Web3Forms](https://web3forms.com) (free, no account backend needed beyond
their site). Right now both are placeholders:

- Open `index.html`
- Search for `PASTE-YOUR-WEB3FORMS-KEY-HERE` — it appears **twice**, once
  in the contact form near the bottom of the page, once in the recruiter
  document-unlock form.
- Sign up free at web3forms.com, verify your email, and you'll get an
  access key (a UUID-looking string).
- Replace both instances of `PASTE-YOUR-WEB3FORMS-KEY-HERE` with that key.

Until you do this, both forms will show an error message when submitted —
the page itself works fine, but nothing will actually reach your inbox.

## Making updates yourself

### Replace your résumé / PDFs
Drop a new PDF into `assets/` and either:
- keep the exact same filename (simplest — no HTML changes needed), or
- use a new filename and update the matching `href="assets/..."` line in
  `index.html` (search for the old filename, there's one link per document
  in the recruiter modal near the bottom of the file).

### Replace your profile photo
Replace `assets/enam1.jpg` (homepage, beside your name) or
`assets/enam2.jpg` ("Meet the Engineer" card) with a new image — keep the
same filename and the site updates automatically. If you use a different
filename, update the matching `<img src="assets/...">` tag in `index.html`.
Recommended: keep photos under ~200KB (resize to roughly 600–800px wide,
JPEG quality ~80) so the page loads fast.

### Update your achievements / metrics / case studies
All the text content lives directly in `index.html` — there's no separate
data file or CMS. Open it in any text editor and search for the section you
want to change (e.g. search "Dwg. no. SQE-01" for the first case study, or
"gauge-row" for the metrics dashboard). Edit the text between the HTML
tags; leave the tags themselves alone.

### Change your Web3Forms key
Covered above — search `PASTE-YOUR-WEB3FORMS-KEY-HERE` in `index.html`,
replace both occurrences.

## Files you should never rename

Renaming these breaks something unless you also update the reference to
match:

- `index.html` — must keep this exact name; it's what GitHub
  Pages/Netlify/Vercel look for automatically at the root.
- `assets/` — the folder name itself is referenced throughout
  `index.html` (e.g. `assets/enam1.jpg`). Renaming the folder breaks every
  image and PDF on the page.
- `robots.txt` and `sitemap.xml` — search engines look for these exact
  filenames at your site's root; renaming them means they're never found.
- Any file inside `assets/` you rename must also be updated in the matching
  `href=` or `src=` line inside `index.html` — see "Making updates
  yourself" above.

## Notes

- This site is fully static — there's no server-side code, database, or
  login system. The "Recruiter" document unlock is a lead-capture form
  (name/designation/organization go to your inbox via Web3Forms), not real
  access control — treat it as a polite gate, not a security boundary.
- For visitor analytics (page views, downloads, time on page), consider
  adding a privacy-friendly analytics script such as
  [Plausible](https://plausible.io) or [Fathom](https://usefathom.com) —
  either is a single `<script>` tag added to the `<head>` of `index.html`,
  with a real dashboard on their end.
