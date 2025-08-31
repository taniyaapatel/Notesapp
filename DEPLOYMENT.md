# Deployment Guide for Vercel

## Prerequisites
- Your app is working locally with MongoDB
- You have a Vercel account
- Your MongoDB Atlas cluster is configured

## Step 1: Set Environment Variables in Vercel

1. Go to your Vercel dashboard
2. Select your project
3. Go to **Settings** → **Environment Variables**
4. Add the following environment variable:

```
Name: MONGODB_URI
Value: mongodb+srv://username:password@cluster.mongodb.net/notesapp?retryWrites=true&w=majority
Environment: Production (and Preview if you want)
```

**Important:** Replace the connection string with your actual MongoDB Atlas connection string.

## Step 2: Verify MongoDB Atlas Settings

1. Go to MongoDB Atlas dashboard
2. Click on **Network Access**
3. Ensure you have **0.0.0.0/0** (Allow access from anywhere) or add Vercel's IP ranges
4. Go to **Database Access** and ensure your user has read/write permissions

## Step 3: Deploy to Vercel

1. Push your code to GitHub/GitLab
2. Connect your repository to Vercel
3. Deploy

## Step 4: Test the API

After deployment, test your API endpoints:

- Health check: `https://your-app.vercel.app/api/health`
- Create note: `POST https://your-app.vercel.app/api/notes`

## Common Issues & Solutions

### Issue: "Error saving notes"
**Cause:** MongoDB connection failed
**Solution:** Check your MONGODB_URI environment variable in Vercel

### Issue: "Database not connected"
**Cause:** Environment variable not set or MongoDB connection string invalid
**Solution:** Verify MONGODB_URI in Vercel dashboard

### Issue: CORS errors
**Cause:** Frontend trying to access backend from different domain
**Solution:** Your CORS is already configured to allow all origins

## Environment Variables Reference

```bash
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/notesapp?retryWrites=true&w=majority
NODE_ENV=production
```

## Testing Locally vs Production

- **Local:** Uses `.env` file
- **Production:** Uses Vercel environment variables
- **Debug:** Check Vercel function logs for detailed error messages
