# Sitewise Studio website

**Smart websites for every story.** Static website for [sitewisestudio.site](https://sitewisestudio.site).

Plain HTML + CSS + a little vanilla JS. No frameworks, no build step. Hosted free on GitHub Pages.

## Files

| Path | What it is |
|---|---|
| `index.html` | Main landing page (hero, services, ownership, work, process, packages, FAQ, contact) |
| `thank-you.html` | Page shown after the contact form is sent |
| `404.html` | "Page not found" page (GitHub Pages uses it automatically) |
| `privacy.html`, `terms.html`, `refund.html`, `delivery.html` | Policy pages (needed for Razorpay website verification) |
| `css/style.css` | All styles. Brand colours are at the top under `:root` |
| `js/main.js` | Mobile menu, package pre-select, smooth scroll, current year, scroll animations |
| `assets/` | Logos, OG/share image (`og-image.png` 1200x630, source `og-image.svg`) |
| `favicon.*`, `apple-touch-icon.png`, `icon-192/512.png`, `site.webmanifest` | Browser and phone icons |
| `CNAME` | Tells GitHub Pages to use `sitewisestudio.site` |
| `robots.txt`, `sitemap.xml` | For search engines |

To preview locally, open `index.html` in a browser. Or run `npx serve .` and open the URL it prints. Note: `404.html` uses root paths (`/css/...`), so it only looks right on the live site or a local server.

## 1. Turn on GitHub Pages

1. Push this repo to GitHub (branch `main`).
2. Go to the repo **Settings → Pages**.
3. Under **Build and deployment**, choose **Source: Deploy from a branch**.
4. Choose branch **`main`** and folder **`/ (root)`**, then **Save**.
5. Under **Custom domain**, enter `sitewisestudio.site` and save. The `CNAME` file in this repo already contains it.

## 2. DNS records at your domain registrar

In your registrar's DNS settings (wherever you bought `sitewisestudio.site`), add these records and remove any old A/AAAA records for `@` that point somewhere else:

| Type | Host / Name | Value |
|---|---|---|
| A | `@` | `185.199.108.153` |
| A | `@` | `185.199.109.153` |
| A | `@` | `185.199.110.153` |
| A | `@` | `185.199.111.153` |
| CNAME | `www` | `<your-github-username>.github.io` |

Optional IPv6 (AAAA records for `@`): `2606:50c0:8000::153`, `2606:50c0:8001::153`, `2606:50c0:8002::153`, `2606:50c0:8003::153`.

DNS changes can take anywhere from a few minutes to 24 hours to work. GitHub's docs: <https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site>

## 3. Enforce HTTPS

Once the DNS check in **Settings → Pages** shows a green tick, tick **Enforce HTTPS**. If the box is greyed out, wait a little while GitHub issues the certificate, then try again.

## 4. Activate the contact form (FormSubmit)

The form sends enquiries to **sitewisestudio.site@gmail.com** through [FormSubmit](https://formsubmit.co). You don't need a backend or an account.

1. After the site is live, fill in the contact form yourself and submit it.
2. FormSubmit sends an **activation email** to sitewisestudio.site@gmail.com. Check Spam/Promotions if you don't see it.
3. Click **Activate Form** in that email. From then on, every enquiry arrives in your Gmail as a table.

Spam protection: there's a hidden `_honey` honeypot field, plus FormSubmit's own captcha step. After a successful send, visitors are taken to `thank-you.html`.

> Tip: after activation, FormSubmit gives you a random alias for your email. You can replace `sitewisestudio.site@gmail.com` in the form's `action` URL with that alias to hide your address from spam bots.

## 5. Placeholders you must replace

Search the whole project (in VS Code: Ctrl/Cmd + Shift + F) and replace these:

- [ ] **WhatsApp number**: replace `91XXXXXXXXXX` (appears in every `.html` file) with your number in international format with no `+`, spaces or dashes, e.g. `919876543210`. Links look like `https://wa.me/919876543210`.
- [ ] **City**: replace `[YOUR CITY, STATE]` in `index.html` (Contact → Location card), e.g. `Kolkata, West Bengal`.
- [ ] Optional: add your city to the JSON-LD block in the `<head>` of `index.html` (`"address"` → add `"addressLocality"` and `"addressRegion"`).
- [ ] **Policy pages**: each one starts with an HTML comment saying it is a template. Read all four and edit them to match how you actually work. Update the "Last updated" date when you change them.
- [ ] **Sample work**: the three Work cards are labelled "Sample concept". Replace them with real projects (screenshots + client permission) once you have them.

## 6. Razorpay (later)

In `index.html`, search for `RAZORPAY PAYMENT BUTTON GOES HERE`. Below it is a hidden **Pay Online** section:

1. Create a **Payment Button** in the Razorpay Dashboard.
2. Paste its embed code inside `<div class="pay-online__button">`.
3. Remove the `hidden` attribute from `<section class="pay-online" id="pay-online" ... hidden>`.

Never put Razorpay secret keys in this repo. The Payment Button embed code is safe to publish.

## Editing tips

- **Colours**: change the variables at the top of `css/style.css`. Keep navy text on coral buttons (white on coral fails contrast) and use `#C9441C` for small coral text on light backgrounds.
- **Packages**: the "Ask for price" buttons use `data-package="Starter"` (etc.) to pre-select the package in the form. The service cards use `data-need="..."`. The values must exactly match an `<option value>` in the form.
- **Links from other pages** can pre-select too: `index.html?package=Premium#contact`.
- **Sitemap**: if you add a page, add it to `sitemap.xml`.
- **Share preview image**: `assets/og-image.png`. Edit `assets/og-image.svg` and export it at 1200x630 if you change it.
