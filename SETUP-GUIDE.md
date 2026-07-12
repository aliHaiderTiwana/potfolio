# Setup Guide

Your portfolio has three parts:

- `index.html` — the public site
- `admin.html` — your private panel for adding projects/skills (not linked anywhere on the public site)
- `data/projects.json` and `data/skills.json` — the content the public site reads; `admin.html` edits these by committing to GitHub

Do these four things before you share the link.

## 1. Change the admin passphrase

Open `admin.html`, find this line near the top of the `<script>` block:

```js
if(val === 'letmein-change-this'){
```

Replace `letmein-change-this` with your own passphrase. This isn't real security by itself — anyone who views the page source can read it — it just keeps casual visitors out. Your actual protection is step 2.

## 2. Create a GitHub personal access token (this is the real access control)

1. Go to **github.com → Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token**.
2. Give it a name like `portfolio-admin`.
3. Under **Repository access**, choose **Only select repositories** and pick just your portfolio repo.
4. Under **Permissions → Repository permissions**, set **Contents** to **Read and write**. Leave everything else as "No access."
5. Generate the token and copy it somewhere safe (GitHub only shows it once).

You'll paste this token into `admin.html` each time you use it (or check "Remember on this device" to save it in that browser only — never share a screen recording or screenshot with the token visible).

## 3. Set up your free contact form (Formspree)

The contact form needs somewhere to send submissions since there's no backend server.

1. Go to **formspree.io** and create a free account (50 submissions/month free).
2. Create a new form, and copy the endpoint it gives you, e.g. `https://formspree.io/f/abcd1234`.
3. Open `index.html`, find:
   ```html
   <form id="contactForm" class="contact-form" action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
   ```
4. Replace `YOUR_FORM_ID` with your real endpoint.

## 4. Fill in your real links

In `index.html`, replace the placeholders:
- `https://github.com/alihaider` → your real GitHub
- `https://linkedin.com/in/alihaider` → your real LinkedIn
- `ali.haider@example.com` → your real email
- `/resume.pdf` → upload your actual resume PDF into the project folder as `resume.pdf`

---

## Hosting it for free (GitHub Pages)

1. Create a new **public** GitHub repository, e.g. `portfolio`.
2. Upload all these files to it, keeping the folder structure:
   ```
   index.html
   admin.html
   robots.txt
   data/projects.json
   data/skills.json
   resume.pdf   (add this yourself)
   ```
3. Go to the repo's **Settings → Pages**.
4. Under **Build and deployment → Source**, choose **Deploy from a branch**, pick `main` and `/ (root)`, then **Save**.
5. After a minute or two, GitHub gives you a live link:
   `https://<your-username>.github.io/<repo-name>/`

That's the link you share. Your admin panel lives at:
`https://<your-username>.github.io/<repo-name>/admin.html`
— reachable by direct URL only, never linked from the site itself.

### Alternatives (also free)
- **Vercel** or **Netlify** — connect your GitHub repo, they auto-deploy on every commit (including ones `admin.html` makes), and give you a similarly clean URL. Slightly faster to update than GitHub Pages' occasional caching delay.
- Any of these work with this project as-is — it's plain HTML/CSS/JS, no build step required.

### Using your own domain (optional)
All three hosts let you attach a custom domain for free (you only pay for the domain itself, e.g. via Namecheap or Google Domains) — look for "Custom domain" in the hosting settings.
