# Production Deployment Guide

## Vercel Environment Variables

Add these environment variables in your Vercel project settings:

### Required for App
```
SHOPIFY_API_KEY=your_api_key
SHOPIFY_API_SECRET=your_api_secret
SHOPIFY_APP_URL=https://daily-toolkit-five.vercel.app
SCOPES=write_products,read_themes
```

### Required for Database (Prisma Session Storage)
```
DATABASE_URL=postgresql://postgres:[PASSWORD]@db.[PROJECT_REF].supabase.co:5432/postgres
```

To get your `DATABASE_URL`:
1. Go to Supabase Dashboard → Project Settings → Database
2. Copy the "Connection string" URI format
3. Replace `[PASSWORD]` with your database password

### Alternative: Supabase Connection (if not using DATABASE_URL)
```
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_SERVICE_ROLE_KEY=your_service_role_key
```

## Supabase Database Setup

1. Go to Supabase SQL Editor
2. Run the contents of `prisma/supabase-schema.sql`
3. This creates all required tables including `Session`, `tool_settings`, `bundle_configs`, `reviews`

## Deploy Steps

1. Push code to GitHub
2. Vercel will auto-deploy
3. The build command will:
   - Use PostgreSQL schema
   - Generate Prisma client
   - Build the app

## Local Development

```bash
# Uses SQLite automatically
npm run dev
```

## Switching Database Schemas Manually

```bash
# For PostgreSQL (production)
npm run schema:use:postgres

# For SQLite (local dev)
npm run schema:use:sqlite
```
