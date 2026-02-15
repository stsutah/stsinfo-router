# STS Utah Router (Vercel Proxy)

This is a proxy/router project that serves content from two separate GitHub repositories at:
- `stsutah.info/pm` → Little Tom Project Manager
- `stsutah.info/bmd` → MSP Business Management Dashboard

## Setup Instructions

### Step 1: Deploy Both Apps First

1. **Deploy Little Tom PM** (`stsutah/liltom-PM`)
   - Go to https://vercel.com/new
   - Import the repo
   - Deploy (zero config needed)
   - **Copy the production URL** (e.g., `liltom-pm-xyz.vercel.app`)

2. **Deploy MSP Dashboard** (`stsutah/STS-BMD`)
   - Go to https://vercel.com/new
   - Import the repo
   - Framework: Vite
   - Root Directory: `frontend`
   - Build Command: `npm run build`
   - Output Directory: `dist`
   - Deploy
   - **Copy the production URL** (e.g., `sts-bmd-abc.vercel.app`)

### Step 2: Update vercel.json

Replace the placeholder URLs in `vercel.json`:
```json
"destination": "https://YOUR_ACTUAL_PM_URL/:match*"
"destination": "https://YOUR_ACTUAL_BMD_URL/:match*"
```

### Step 3: Deploy This Router

1. Push this repo to GitHub (e.g., `stsutah/router`)
2. Import to Vercel as a new project
3. Deploy (no build config needed)

### Step 4: Add Custom Domain

1. In Vercel dashboard for the router project:
2. Go to Settings → Domains
3. Add `stsutah.info`
4. Follow DNS setup instructions

### Step 5: Test

- https://stsutah.info/ → Landing page
- https://stsutah.info/pm → Kanban dashboard
- https://stsutah.info/bmd → MSP dashboard

## Important Notes

- The PM and BMD apps should NOT have `stsutah.info` set as their domain
- They remain on their `*.vercel.app` URLs
- Only this router project uses the custom domain
- All routing happens via Vercel's rewrite rules (no redirects, SEO-friendly)

## File Structure

```
stsutah-router/
├── vercel.json       # Routing rules
├── index.html        # Landing page at root
└── README.md         # This file
```

## Troubleshooting

If paths don't work:
1. Verify the destination URLs in vercel.json are correct
2. Check that both apps deployed successfully
3. Make sure the router project has the custom domain (not the apps)
4. Test the apps directly at their *.vercel.app URLs first

---

Built for STS Utah development environment.
