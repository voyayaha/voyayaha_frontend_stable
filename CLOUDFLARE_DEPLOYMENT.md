# Voyayaha — Cloudflare Workers deployment

## Cloudflare settings

Root directory:
`voyayaha_frontend_stable`

Build system version:
`3`

Build command:
`npm run build`

Deploy command:
`npx wrangler deploy`

Node.js version:
`22`

The project contains `package-lock.json` and does not require Bun. The `.nvmrc` pins Node 22 for the build environment.

## Production environment variables

Set these in Cloudflare → Workers & Pages → Voyayaha → Settings → Variables and Secrets → Production:

`VITE_TRAVEL_API_BASE_URL=https://voyayaha-backend-stable.onrender.com`

`VITE_WORDPRESS_API_BASE_URL=https://voyayaha.com`

`VITE_*` variables are embedded at build time, so redeploy after changing them.

## API routing

The browser uses same-origin TanStack Start routes:

- `/api/social-discovery`
- `/api/travel-memories`
- `/api/travel-memory`
- `/api/travel-intel`
- `/api/village-experiences`
- `/api/hidden-experiences`
- `/api/itinerary`

Those server routes call the stable Render backend:
`https://voyayaha-backend-stable.onrender.com`

The browser should not call the Render backend directly for these features.

## Render backend

Set these environment variables on the stable Render backend as required by the backend:

`VOYAYAHA_WORDPRESS_URL=https://voyayaha.com`

`VOYAYAHA_WORDPRESS_VERIFY_TLS=false`

If `CORS_ORIGINS` is configured on Render, include:

`https://voyayaha.voyayaha.workers.dev`

The backend source also includes that Worker origin in its default CORS list.
