# Render Deployment Guide

## Issue: Dockerfile Not Found

If you're seeing the error:
```
error: failed to solve: failed to read dockerfile: open Dockerfile: no such file or directory
```

This means Render is checking out an old commit that doesn't include the Dockerfile.

## Solution

### Option 1: Manual Redeploy (Recommended)
1. Go to your Render dashboard
2. Navigate to your web service
3. Click **Manual Deploy** → **Deploy latest commit**
4. This will force Render to use the latest commit from the `main` branch

### Option 2: Check Branch/Commit Settings
1. In Render dashboard, go to your service settings
2. Under **Build & Deploy**, check:
   - **Branch**: Should be `main` (not a specific commit SHA)
   - **Auto-Deploy**: Should be enabled
3. If a specific commit is pinned, remove it and use `main` branch instead

### Option 3: Recreate Service
If the above doesn't work:
1. Delete the existing service in Render
2. Create a new Web Service
3. Connect to: `https://github.com/txlcodes/stone-arts`
4. Ensure branch is set to `main`
5. Render will auto-detect the Dockerfile

## Verify Latest Commit

The Dockerfile was added in commit `5071739` and updated in `f9847b6`. 

To verify you're on the latest commit:
```bash
git log --oneline -3
```

You should see:
```
f9847b6 Add nginx configuration for better static file handling
5071739 Add Dockerfile and Render configuration for deployment
d2bf5b9 Initial commit: stonearts webshop frontend codebase
```

## Files Required for Deployment

- ✅ `Dockerfile` - Docker configuration
- ✅ `nginx.conf` - Nginx server configuration  
- ✅ `render.yaml` - Render service configuration
- ✅ `.dockerignore` - Docker build exclusions

All files are in the latest `main` branch commit.

