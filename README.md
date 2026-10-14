# Murmur landing page

A static, single-file site. No build step. Files:

- `index.html` – the page (styles and scripts are inline)
- `favicon.svg`, `favicon-32.png`, `apple-touch-icon.png` – icons
- `og.png` – 1200×630 social preview image
- `CNAME` – custom domain file for GitHub Pages (edit or delete, see step 5)

## 1. Set your real domain in the page (do this first)

The social preview tags need absolute URLs. `index.html` currently uses the
placeholder `https://murmur.example`. Replace it everywhere with your real
address, for example `https://www.yourdomain.com` or
`https://YOUR-USER.github.io/murmur`:

    sed -i 's#https://murmur.example#https://www.yourdomain.com#g' index.html

Four tags use it: `canonical`, `og:url`, `og:image`, `twitter:image`.
Facebook, LinkedIn, Slack and X will not show the preview image until these
point at a live address.

## 2. Put it on GitHub

    cd murmur-site
    git init -b main
    git add .
    git commit -m "Murmur landing page"
    gh repo create murmur --public --source=. --push

(No `gh`? Create an empty public repo on github.com, then
`git remote add origin <url>` and `git push -u origin main`.)

## 3. Turn on GitHub Pages

Repository > **Settings** > **Pages** > Source: **Deploy from a branch** >
Branch: `main`, folder `/ (root)` > **Save**. After a minute the site is live at
`https://YOUR-USER.github.io/murmur/`.

## 4. Custom domain (optional)

At your DNS provider:

- **Subdomain** (for example `www.yourdomain.com`): add a `CNAME` record
  pointing to `YOUR-USER.github.io`.
- **Apex domain** (`yourdomain.com`): add four `A` records to GitHub Pages'
  addresses, listed at
  <https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site>.
  Check that page for the current values.

## 5. Tell GitHub the domain

Put your domain in the `CNAME` file (one line, no `https://`), commit and
push. Or set it under Settings > Pages > Custom domain. Then tick
**Enforce HTTPS** once the certificate is issued (can take up to an hour).
If you use only the github.io address, delete the `CNAME` file.

## 6. Check the social preview

After deploying, paste your URL into a link debugger to refresh any cache:

- Facebook: <https://developers.facebook.com/tools/debug/>
- LinkedIn: <https://www.linkedin.com/post-inspector/>

## Other hosts

Netlify Drop, Cloudflare Pages and Vercel all accept this folder as is.
Deploy it with no build command and `/` as the output directory.

## Things still to wire up

- "Generate demo key" only makes a random string in the browser.
- Footer links (Contact, Terms, Privacy) point back to the page.
- API and MCP URLs in the code samples (`api.murmur.example`) are placeholders.
