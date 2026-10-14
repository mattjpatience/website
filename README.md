# mattpatience.com

Personal academic website of Matthew Patience. Plain HTML, hosted free on GitHub Pages, with DNS on Cloudflare (free plan). The domain stays registered with HostGator (Launchpad), paid through June 10, 2027.

## Files in this repository

| File | What it is |
|---|---|
| `index.html` | The whole website (one page) |
| `Patience_CV.pdf` | Your CV. Every CV button on the site links to this file name. |
| `CNAME` | Created automatically by GitHub when you set the custom domain. Don't delete it. |

---

## The move, in five phases

### Phase 1: Put the site on GitHub (about 15 minutes)

1. Go to https://github.com/signup and create a free account. Pick a username you'd be happy to have public (for example `mattpatience`). Verify your email when GitHub asks.
2. Click the **+** at the top right → **New repository**.
   - Repository name: `website`
   - Visibility: **Public** (free Pages sites must be public)
   - Leave everything else unticked → **Create repository**.
3. On the empty repository page, click **uploading an existing file**. Drag in:
   - `index.html`
   - `README.md`
   - your CV, renamed to exactly `Patience_CV.pdf`

   Click **Commit changes**.
4. Go to the repository's **Settings → Pages**. Under *Build and deployment*: Source **Deploy from a branch**, Branch **main**, folder **/ (root)** → **Save**.
5. After a minute or two, the site is live at `https://YOUR-USERNAME.github.io/website/`. Check it before going further.

### Phase 2: Set up Cloudflare (about 10 minutes)

1. Create a free account at https://dash.cloudflare.com/sign-up.
2. Go to **Domains → Onboard a domain**, enter `mattpatience.com`, let Cloudflare scan your existing records, and choose the **Free** plan.
3. On the DNS records review screen:
   - **Delete** every record that points to `192.185.48.226` (the HostGator server), plus the **MX** record. You don't use domain email, and these will stop working once the hosting is cancelled anyway.
   - **Add** four **A** records, name `@`, proxy status **DNS only** (gray cloud):
     ```
     185.199.108.153
     185.199.109.153
     185.199.110.153
     185.199.111.153
     ```
   - **Add** one **CNAME** record: name `www`, target `YOUR-USERNAME.github.io`, proxy status **DNS only** (gray cloud).
   - Gray cloud matters: GitHub needs to see these records directly to issue your HTTPS certificate.
4. Cloudflare then shows you **two nameservers** (they end in `ns.cloudflare.com`). Keep that tab open.

### Phase 3: Point the domain at Cloudflare (5 minutes, then a wait)

1. Log in to the HostGator Customer Portal: https://portal.hostgator.com/login
2. Open the **Domain Name** tab → **Advanced tools** → **Manage** next to **Nameservers** → **Continue**.
3. Replace `ns1655.hostgator.com` and `ns1656.hostgator.com` with the two Cloudflare nameservers → **Save**.
4. Back in Cloudflare, click **Check nameservers**. Cloudflare emails you when the domain is active. This usually takes under an hour but can take up to 24.

### Phase 4: Connect the domain in GitHub (5 minutes, then a short wait)

1. In the repository: **Settings → Pages → Custom domain**, enter `mattpatience.com` → **Save**. GitHub adds a `CNAME` file to the repository for you.
2. Wait for the DNS check to show a green tick, then tick **Enforce HTTPS**. The certificate can take up to an hour to appear.
3. Visit https://mattpatience.com. You should see the new site.

### Phase 5: Retire the WordPress hosting

Only after the new site is live at https://mattpatience.com:

1. Optional: in cPanel, download a backup of the old WordPress site.
2. Cancel the **hosting plan** at HostGator. Keep the **domain registration**. Tell HostGator support explicitly if needed: cancel hosting, keep the domain.
3. Note the domain renewal date (June 10, 2027). You can renew at HostGator, or later transfer the registration to Cloudflare Registrar, which charges cost price.

---

## Updating the site later

- **Edit text:** open `index.html` on GitHub, click the pencil icon, make the change, and click **Commit changes**. The live site updates within a minute or two.
- **New CV:** upload a new file named exactly `Patience_CV.pdf`. It replaces the old one, and every CV link keeps working.
- **New publication:** copy an existing `<li>…</li>` line in the Publications section and edit the text.

## References

- GitHub: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site
- Cloudflare: https://developers.cloudflare.com/learning-paths/get-started/add-domain-to-cf
- HostGator: https://www.hostgator.com/help/article/changing-name-servers-with-launchpad
