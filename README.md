# abdelrahman.dev — portfolio

Single-page portfolio site. No build step, no dependencies — pure HTML/CSS/JS.

## Structure

```
index.html      the whole site
favicon.svg     tab icon
og.svg          social link-preview image
404.html        not-found page
vercel.json     static-site config (clean URLs)
```

## Deploy on Vercel (recommended — free)

**Option A — no GitHub, fastest:**
1. Install the CLI once: `npm i -g vercel`
2. From this folder, run: `vercel`
3. Follow the prompts (pick any project name, accept defaults — it's a static site, no build command needed)
4. Run `vercel --prod` to push it live

**Option B — via GitHub (recommended if you'll keep editing it):**
1. Push this folder to a new GitHub repo
2. Go to [vercel.com/new](https://vercel.com/new), import the repo
3. Framework preset: **Other** (or "No framework") — leave build command empty, output directory as root `.`
4. Deploy. Vercel gives you a `*.vercel.app` URL immediately; add a custom domain later in Project Settings → Domains

## Deploy on GitHub Pages (also free)

1. Push this folder to a repo named `<your-username>.github.io` (for a root domain) or any repo name (for a `/reponame` path)
2. Go to Settings → Pages → Source → deploy from branch `main`, folder `/ (root)`
3. Site goes live at `https://<username>.github.io` (or `/reponame`) within a minute or two

## Before going live

- [ ] Terminal `contact` command and the contact button both link to `https://t.me/Abdelrahmann17` — confirm that's correct
- [ ] Swap `og.svg` for a `.png`/`.jpg` if you want previews on platforms that don't render SVG in link cards (Twitter/X sometimes doesn't) — easiest: screenshot the hero section
- [ ] If you buy a custom domain, add it in Vercel/GitHub Pages settings and update `og:image`/`twitter:image` to an absolute URL (currently relative — works once a domain is attached)

## Local preview

No server needed — just open `index.html` directly in a browser, or run any static server:

```
npx serve .
```

## AI portfolio agent

The hero interaction uses an OpenRouter-backed serverless endpoint at `/api/chat`. The API key is **never put in the browser**.

### Vercel setup

1. Import the repo into Vercel.
2. In **Project Settings → Environment Variables**, add:
   - `OPENROUTER_API_KEY` — your OpenRouter API key
   - `OPENROUTER_MODEL` — optional; defaults to `openrouter/free`
   - `SITE_URL` — optional; your deployed site URL
3. Redeploy.

OpenRouter's chat completions endpoint uses a Bearer API key and supports the `HTTP-Referer` and `X-Title` attribution headers. The free router can be used with `openrouter/free`; model availability can change over time.

**Important:** GitHub Pages alone cannot run `/api/chat`, because it only hosts static files. Keep the code in GitHub and deploy the same repository on Vercel (or another serverless host) for the AI agent to work.


## AI usage protection

The portfolio agent is limited to **15 AI replies per IP address per 24 hours**. The server enforces this before making an OpenRouter request, so hitting the limit does not consume another model response.

For production on Vercel, connect an Upstash Redis database and set `UPSTASH_REDIS_REST_URL` and `UPSTASH_REDIS_REST_TOKEN`. This makes the limit shared across serverless instances. If those variables are absent, the API falls back to a best-effort in-memory limiter for local/development use.

After a few useful exchanges the UI nudges visitors toward contacting Abdelrahman, and after 15 replies the agent stops making model requests and gives them the contact link.

The agent is intentionally portfolio-only and solution-oriented: it should not dismiss custom project ideas. It connects requests to demonstrated skills and explains a plausible approach without falsely claiming prior experience.
