# SparkMash - Setup Instructions

## 📁 Project Structure

Create this folder structure on your computer:

```
sparkmash/
├── index.html           (Your React app - export from Claude artifact)
├── api/
│   └── expand-idea.js   (Serverless function for OpenAI)
├── vercel.json          (Vercel configuration)
├── package.json         (Project metadata)
└── README.md            (Project documentation)
```

## 🚀 Step-by-Step Deployment

### 1. Prepare Your Files

1. **Save the React app** from the artifact as `index.html`
2. **Create an `api` folder** in your project root
3. **Copy the `expand-idea.js`** file into the `api` folder
4. **Add `vercel.json`** and `package.json`** to the root

### 2. Initialize Git Repository

```bash
cd /path/to/sparkmash
git init
git add .
git commit -m "Initial commit - SparkMash with PRD expansion"
```

### 3. Push to GitHub

```bash
# Create a new repository on GitHub (https://github.com/new)
# Name it: sparkmash
# Don't initialize with README

# Then run:
git remote add origin https://github.com/YOUR_USERNAME/sparkmash.git
git branch -M main
git push -u origin main
```

### 4. Deploy to Vercel

#### Option A: Using Vercel Website (Easiest)

1. Go to [vercel.com](https://vercel.com) and sign up/login
2. Click **"Add New Project"**
3. **Import your GitHub repository** (sparkmash)
4. Vercel will auto-detect settings - click **"Deploy"**
5. Wait for deployment to complete

#### Option B: Using Vercel CLI

```bash
# Install Vercel CLI globally
npm i -g vercel

# Login to Vercel
vercel login

# Deploy
vercel

# Follow the prompts:
# - Set up and deploy? Yes
# - Which scope? (your account)
# - Link to existing project? No
# - Project name: sparkmash
# - Directory: ./
# - Override settings? No

# Deploy to production
vercel --prod
```

### 5. Add Environment Variable (CRITICAL!)

After deployment:

1. Go to your project dashboard on Vercel
2. Click **"Settings"** tab
3. Click **"Environment Variables"** in the left sidebar
4. Add a new variable:
   - **Name:** `OPENAI_API_KEY`
   - **Value:** Your OpenAI API key (sk-...)
   - **Environment:** Select all (Production, Preview, Development)
5. Click **"Save"**

6. **Redeploy** the project (go to Deployments tab → click the 3 dots on latest → "Redeploy")

### 6. Update Your Domain (Optional)

If you want to use sparkmash.com:

1. In Vercel project settings → **Domains**
2. Click **"Add Domain"**
3. Enter `sparkmash.com`
4. Follow Vercel's instructions to update your DNS records
5. Also add `www.sparkmash.com` as an alias

## 🔧 Testing Locally

```bash
# Install Vercel CLI if you haven't
npm i -g vercel

# Create .env file in your project root
echo "OPENAI_API_KEY=your-api-key-here" > .env

# Run local development server
vercel dev

# Visit http://localhost:3000
```

## ⚠️ Important Notes

### Security
- ✅ Your OpenAI API key is stored securely in Vercel environment variables
- ✅ It's NEVER exposed in the client-side code
- ✅ Users can't see or access your key

### API Costs
- The OpenAI API will be called each time someone clicks "Expand to PRD"
- Using GPT-4o costs approximately $0.005-0.015 per PRD (depending on length)
- Monitor your usage at [platform.openai.com/usage](https://platform.openai.com/usage)
- Consider adding rate limiting if the app gets heavy traffic

### Rate Limiting (Optional - for production)
If you want to add rate limiting to prevent abuse, you can use Vercel's Edge Middleware or Upstash Redis. Let me know if you need help with this!

## 🐛 Troubleshooting

### "Failed to generate PRD" error
- Check that your `OPENAI_API_KEY` environment variable is set correctly in Vercel
- Verify your OpenAI API key is valid and has credits
- Check the Vercel function logs (Functions tab in dashboard)

### Ideas generate but PRD expansion doesn't work
- Make sure you redeployed after adding the environment variable
- Check browser console for errors (F12 → Console tab)
- Verify the API route is accessible: `https://your-app.vercel.app/api/expand-idea`

### Local development not working
- Ensure `.env` file exists in project root with your API key
- Run `vercel dev` (not just `vercel`)
- Check that port 3000 isn't already in use

## 📚 Next Steps

Once deployed:
1. Test all features thoroughly
2. Share with friends and get feedback
3. Monitor API usage and costs
4. Consider adding features like:
   - Saving favorite ideas
   - Sharing PRDs via link
   - Exporting PRDs as PDF
   - Adding more expansion types (pitch deck, marketing plan, etc.)

## 🆘 Need Help?

If you run into issues:
1. Check Vercel's function logs in the dashboard
2. Look at browser console for client-side errors
3. Verify all files are in the correct locations
4. Make sure environment variable is set and project is redeployed

---

**You're all set! 🎉** Your SparkMash app is now live with secure API integration!