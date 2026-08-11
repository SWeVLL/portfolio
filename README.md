# Abdelrahman — Systems Builder

> Personal portfolio for Abdelrahman, focused on AI systems, agents, mobile applications, and real-time backends.

**Live site:** [Deploy with Vercel](https://vercel.com/)

The portfolio is a single-page, responsive site with an interactive AI assistant that helps visitors explore the work and encourages serious project inquiries.

## What is here

- Responsive portfolio UI for desktop, tablet, and mobile
- Swipeable section navigation on smaller screens
- Interactive portfolio AI assistant
- Project and skills presentation
- Contact-focused visitor flow
- Custom 404 page, favicon, and social preview asset
- Vercel serverless API endpoint for the AI assistant

## Featured work

### ALFRED

A local AI-assistant project exploring conversational interaction, memory, voice, and tool-driven workflows.

### NEXUS

An experimental software project centered around building connected AI/software systems and practical backend infrastructure.

See the portfolio itself for the current project descriptions and implementation details.

## Tech

The portfolio is intentionally lightweight:

- HTML
- CSS
- JavaScript
- Vercel serverless functions
- OpenRouter for the portfolio assistant
- Upstash Redis for production rate limiting

The site has no frontend framework or build step.

## Run locally

You can preview the static site directly by opening `index.html`.

For a local static server:

```bash
npx serve .
```

The AI endpoint requires the environment variables described below and is intended to run through Vercel's serverless runtime.

## Deploy

### Vercel

Vercel is the recommended deployment target because the site includes `/api/chat`.

1. Import this repository into Vercel.
2. Use **Other / No Framework** as the framework preset.
3. Leave the build command empty.
4. Use the repository root as the output/root directory.
5. Add the required environment variables.
6. Deploy.

### Environment variables

Set these in Vercel Project Settings → Environment Variables:

```text
OPENROUTER_API_KEY=your_key
OPENROUTER_MODEL=openrouter/free
SITE_URL=https://your-domain.example
UPSTASH_REDIS_REST_URL=https://your-database.upstash.io
UPSTASH_REDIS_REST_TOKEN=your_token
```

`OPENROUTER_API_KEY` and `UPSTASH_REDIS_REST_TOKEN` are secrets. **Never commit their real values to GitHub.**

For local development, copy `.env.example` to `.env` and fill in the values. Keep `.env` out of version control.

## AI assistant

The portfolio assistant is deliberately scoped to the portfolio. Its job is to:

- explain projects and technologies shown on the site
- answer visitor questions using the portfolio context
- discuss how Abdelrahman's demonstrated skills could apply to a new project
- help turn a visitor's idea into a useful starting point
- guide serious visitors toward direct contact

It should not invent previous experience or pretend a project was already completed when it was not.

### Usage protection

The API enforces a limit of **15 AI replies per IP address per 24 hours** before making another model request. In production, Upstash Redis provides shared rate-limit state across Vercel serverless instances.

After the visitor has had useful exchanges, the UI encourages them to contact Abdelrahman directly. Once the limit is reached, the assistant stops making model requests and directs the visitor to contact him.

## Contact

The portfolio currently links the contact flow to:

**Telegram:** [@Abdelrahmann17](https://t.me/Abdelrahmann17)

Update the link in the site if your preferred contact method changes.

## Repository structure

```text
.
├── api/
│   └── chat.js        # serverless AI endpoint
├── index.html          # portfolio UI
├── 404.html            # fallback page
├── favicon.svg         # browser icon
├── og.svg              # social preview artwork
├── vercel.json         # Vercel configuration
├── package.json        # project metadata
└── .env.example        # environment variable template
```

## License

This repository contains a personal portfolio. Unless a separate license is added, the code and design should not be treated as an open-source template for redistribution.
