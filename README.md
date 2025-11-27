# GnosisRamp API Documentation

This directory contains the Mintlify documentation for the GnosisRamp API.

## Local Development

The docs are automatically served at `http://localhost:3001/docs` when you run:

```bash
yarn dev
```

This runs:
- API Server on port 3000
- Dashboard on port 3001
- Mintlify docs on port 3002 (proxied through dashboard at `/docs`)

## Standalone Docs Development

To run just the docs locally without the full application:

```bash
yarn docs:dev
```

The docs will be available at `http://localhost:3002`

## Production Deployment

### Option 1: Deploy to Mintlify (Recommended)

1. **Connect your repository to Mintlify:**
   - Go to [mintlify.com](https://mintlify.com)
   - Connect your GitHub repository
   - Point to the root directory
   - Mintlify will auto-deploy on every push

2. **Update the production URL:**
   - Set the `MINTLIFY_URL` environment variable to your Mintlify deployment URL
   - The dashboard will proxy `/docs` to this URL in production

3. **Example:**
   ```bash
   export MINTLIFY_URL=https://docs.gnosisramp.com
   ```

### Option 2: Self-Host with Static Build

If you prefer to self-host the docs:

1. **Build the docs:**
   ```bash
   yarn docs:build
   ```

2. **Serve the static files:**
   - The build output will be in `.mintlify`
   - You can serve this directory using any static file server
   - Or configure your web server to proxy `/docs` to the static files

3. **Update Next.js config:**
   - Modify `dashboard/next.config.ts` to serve from static files instead of proxying

## Updating API Documentation

1. **Update the OpenAPI spec:**
   - Edit `dashboard/public/openapi.yaml`
   - Copy it to `openapi.yaml`

2. **Regenerate endpoint docs:**
   ```bash
   npx @mintlify/scraping@latest openapi-file openapi.yaml -o api-reference/endpoints
   ```

3. **Update navigation:**
   - If you add/remove endpoints, update the navigation in `docs.json`

## File Structure

```
docs/
├── docs.json              # Configuration and navigation
├── openapi.yaml           # OpenAPI specification
├── api-reference/         # API reference docs
│   ├── overview.mdx       # API reference overview
│   └── endpoints/         # Auto-generated endpoint docs
├── auth/                  # Authentication guides
├── external-accounts/     # External accounts guides
├── intents/              # Intents and compliance guides
├── money-movement/       # Money movement guides
├── webhooks/             # Webhook documentation
└── static/               # Static assets (logos, images)
```

## Mintlify Resources

- [Mintlify Documentation](https://mintlify.com/docs)
- [OpenAPI Setup Guide](https://mintlify.com/docs/api-playground/openapi-setup)
- [Writing Content](https://mintlify.com/docs/content/writing)
