# Railway Deployment Setup Guide

You've already started deploying to Railway! Follow these steps to complete the setup.

## Your Railway Project
Project URL: https://railway.com/project/1a311b48-cd16-4496-b5a8-9f4e8f4c9ce5

---

## Step 1: Add PostgreSQL Database

1. In your Railway project dashboard, click **"+ New"**
2. Select **"Database"** → **"Add PostgreSQL"**
3. Railway will automatically create the database
4. The `DATABASE_URL` will be automatically available to your services

---

## Step 2: Configure Backend Service

### Service Settings

1. Go to your backend service (the one you're currently viewing)
2. Click on **"Settings"** tab
3. Configure:
   - **Root Directory**: `backend`
   - **Start Command**: `uvicorn main:app --host 0.0.0.0 --port $PORT`
   - **Watch Paths**: `backend/**`

### Environment Variables

Click on **"Variables"** tab and add these:

**Required:**
```
DATABASE_URL=${{Postgres.DATABASE_URL}}
GEMINI_API_KEY=your_gemini_api_key_here
ENVIRONMENT=production
PORT=8000
```

**Email Alerts (Optional):**
```
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USERNAME=your_email@gmail.com
SMTP_PASSWORD=your_app_password
SMTP_FROM_EMAIL=your_email@gmail.com
ALERT_RECIPIENT_EMAIL=recipient@example.com
```

**WhatsApp Alerts (Optional):**
```
TWILIO_ACCOUNT_SID=your_twilio_account_sid
TWILIO_AUTH_TOKEN=your_twilio_auth_token
TWILIO_WHATSAPP_FROM=whatsapp:+14155238886
ALERT_RECIPIENT_WHATSAPP=whatsapp:+1234567890
```

**Important Notes:**
- Replace `${{Postgres.DATABASE_URL}}` by selecting it from the "Reference" dropdown
- For Gmail SMTP, you'll need an App Password (not your regular password)
- Twilio credentials are for WhatsApp notifications

---

## Step 3: Add Frontend Service

1. In Railway dashboard, click **"+ New"**
2. Select **"GitHub Repo"** → Choose your repository again
3. Railway will create a new service
4. Configure:
   - **Root Directory**: `/` (leave empty or set to root)
   - **Build Command**: `npm run build`
   - **Start Command**: `npm start`
   - **Watch Paths**: `src/**`, `package.json`

### Frontend Environment Variables

Add in **"Variables"** tab:
```
VITE_API_URL=${{backend.RAILWAY_PUBLIC_DOMAIN}}/api
```

Or manually:
```
VITE_API_URL=https://your-backend-url.up.railway.app/api
```

To get the backend URL:
1. Go to your backend service
2. Click "Settings" → "Networking"
3. Enable "Public Networking"
4. Copy the generated URL

---

## Step 4: Enable Public Access

### For Backend:
1. Go to backend service → **"Settings"** → **"Networking"**
2. Click **"Generate Domain"**
3. Copy the URL (e.g., `https://backend-production-xxxx.up.railway.app`)

### For Frontend:
1. Go to frontend service → **"Settings"** → **"Networking"**
2. Click **"Generate Domain"**
3. This will be your public app URL!

---

## Step 5: Update Backend CORS

After generating the frontend URL, add it to backend allowed origins:

1. Go to backend service → **"Variables"**
2. Add:
```
FRONTEND_URL=https://your-frontend-production-xxxx.up.railway.app
```

3. Update `backend/main.py` CORS settings to use this variable (already configured)

---

## Step 6: Deploy

1. Railway automatically deploys when you push to GitHub
2. Or click **"Deploy"** button in each service
3. Monitor logs in the **"Deployments"** tab

---

## Troubleshooting

### Build Fails

**Backend:**
- Check `backend/requirements.txt` exists
- Verify Python version (should detect Python 3.11+)
- Check deployment logs for specific errors

**Frontend:**
- Check `package.json` exists
- Verify `build` script is defined
- Check Node version compatibility

### Database Connection Errors

1. Ensure PostgreSQL database is added
2. Verify `DATABASE_URL` is correctly referenced: `${{Postgres.DATABASE_URL}}`
3. Check backend logs for connection errors

### Frontend Can't Connect to Backend

1. Verify backend has public domain enabled
2. Check `VITE_API_URL` is correctly set in frontend
3. Verify backend CORS allows frontend domain
4. Check browser console for errors

### Port Issues

Railway automatically provides `$PORT` environment variable. Make sure:
- Backend start command uses `--port $PORT`
- Don't hardcode port 8000

---

## Deployment Checklist

- [ ] PostgreSQL database added
- [ ] Backend service configured with correct root directory
- [ ] Backend environment variables set
- [ ] Backend has public domain enabled
- [ ] Frontend service configured
- [ ] Frontend has correct `VITE_API_URL`
- [ ] Frontend has public domain enabled
- [ ] Both services deployed successfully
- [ ] Database tables created (check backend logs)
- [ ] Can access frontend URL in browser
- [ ] API endpoints responding (test at backend-url/docs)

---

## Testing Your Deployment

### Test Backend API:
1. Go to: `https://your-backend.up.railway.app/docs`
2. You should see FastAPI Swagger documentation
3. Test endpoint: `GET /api/inventory`

### Test Frontend:
1. Go to: `https://your-frontend.up.railway.app`
2. Dashboard should load
3. Try creating an order
4. Check if data syncs properly

---

## Cost & Usage

- **Free Tier**: $5 usage credit per month
- **Estimated Cost**: ~$10-15/month after free credit
  - Backend: ~$5/month
  - Frontend: ~$3/month
  - PostgreSQL: ~$5/month

Track usage in Railway dashboard under **"Usage"** tab.

---

## Automatic Deployments

Railway automatically deploys when you push to GitHub:

```bash
# Make changes locally
git add .
git commit -m "Update feature"
git push origin main

# Railway automatically detects and deploys!
```

---

## Custom Domain (Optional)

1. Go to service → **"Settings"** → **"Networking"**
2. Click **"Custom Domain"**
3. Enter your domain
4. Add CNAME record in your DNS provider:
   - Name: `www` or `@`
   - Value: Railway provided CNAME
5. Wait for DNS propagation (5-60 minutes)

---

## Monitoring & Logs

### View Logs:
1. Click on service
2. Go to **"Deployments"** tab
3. Click on latest deployment
4. View real-time logs

### Restart Service:
1. Go to service
2. Click **"⋮"** menu → **"Restart"**

### Rollback:
1. Go to **"Deployments"** tab
2. Click on previous successful deployment
3. Click **"Redeploy"**

---

## Need Help?

- Railway Docs: https://docs.railway.app
- Railway Discord: https://discord.gg/railway
- Check deployment logs for errors
- Verify environment variables are set correctly

---

## Quick Reference

**Backend URL Pattern:**
```
https://backend-production-[id].up.railway.app
```

**Frontend URL Pattern:**
```
https://frontend-production-[id].up.railway.app
```

**API Documentation:**
```
https://your-backend-url.up.railway.app/docs
```

**Database Connection:**
```
${{Postgres.DATABASE_URL}}
```
