# Cloudflare deployment

This Next.js app uses the OpenNext Cloudflare adapter and needs a PostgreSQL
database for its order, enquiry, and newsletter APIs.

## One-time setup

1. Use Node.js 22.12 or newer and install dependencies with `npm install`.
2. Log in to Cloudflare: `npx wrangler login`.
3. Create a Hyperdrive configuration for the PostgreSQL database:
   `npx wrangler hyperdrive create shilpkaari-db --connection-string="postgres://USER:PASSWORD@HOST:5432/DATABASE"`.
4. Put the Hyperdrive ID returned by Wrangler in `wrangler.jsonc`, replacing
   `REPLACE_WITH_HYPERDRIVE_ID`. Do not commit database credentials.
5. Apply `src/db/schema.ts` to that PostgreSQL database before using the APIs.
6. Set `NEXT_PUBLIC_SITE_URL` to the final HTTPS website URL when building; it
   is embedded in the site's metadata, canonical URL, sitemap, and robots data.
   For example, set it in `.env.production.local` before deployment.

## Preview and deploy

- `npm run preview` builds the OpenNext Worker and runs it locally.
- `npm run deploy` builds and deploys the Worker.
- `npm run upload` builds and uploads a Worker version without deploying it.

For regular local development, set `DATABASE_URL` in `.env.local`; the API
routes use that URL outside the deployed Cloudflare Worker. In Cloudflare, they
use the `HYPERDRIVE` binding.

The project currently references product and workshop images under
`public/images/`, but those files are not included in this project folder.
Add the licensed image assets before launch to avoid broken images and social
preview cards.
