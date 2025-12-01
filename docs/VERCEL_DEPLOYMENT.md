# Vercel Deployment Guide

This guide explains how to deploy the backend service to Vercel from this monorepo.

## Quick Setup

### Option 1: Using Vercel Dashboard (Recommended)

1. **Import your GitHub repository** to Vercel
2. **Configure Project Settings**:
   - **Root Directory**: Set to `backend`
   - **Framework Preset**: Next.js (auto-detected)
   - **Build Command**: Leave empty (Vercel will auto-detect)
   - **Output Directory**: Leave empty (Vercel will auto-detect)
   - **Install Command**: `cd ../.. && pnpm install` (installs from monorepo root)

3. **Environment Variables**: Add all required variables:
   - `NEXT_PUBLIC_SUPABASE_URL`
   - `NEXT_PUBLIC_SUPABASE_ANON_KEY`
   - `SUPABASE_SERVICE_ROLE_KEY`
   - `GEMINI_API_KEY` (optional, for embeddings)
   - `OPENAI_API_KEY` (optional, for chat)
   - `NEXT_TELEMETRY_DISABLED=1`

4. **Deploy**: Click "Deploy"

### Option 2: Using vercel.json (Alternative)

If you prefer using the root-level `vercel.json`, make sure to:
- Set Root Directory to `.` (root) in Vercel settings
- The `vercel.json` will handle the build configuration

## Troubleshooting

### Error: "Cannot find module 'next/dist/compiled/next-server/server.runtime.prod.js'"

This error typically occurs when:
1. Dependencies aren't installed correctly
2. The build is running from the wrong directory
3. Next.js installation is incomplete

**Solution**: 
- Ensure Root Directory is set to `backend` in Vercel project settings
- Ensure Install Command installs from monorepo root: `cd ../.. && pnpm install`
- Check that `pnpm-lock.yaml` is committed to the repository

### Build Fails with "Module not found"

If you see module resolution errors:
- Make sure all workspace dependencies are installed
- Verify `pnpm-workspace.yaml` is in the repository root
- Check that `package.json` files in both root and backend are correct

## Notes

- The `outputFileTracingRoot` in `backend/next.config.js` is only used for Docker builds, not Vercel
- Vercel automatically handles Next.js optimizations
- For production, ensure all environment variables are set in Vercel dashboard

