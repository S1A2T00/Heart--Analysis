# Quick Deployment Commands

## 1. Local Testing
```bash
# Navigate to project
cd Heart_Disease_Analysis_project-main

# Create virtual environment (optional but recommended)
python -m venv venv

# Activate virtual environment
# Windows:
venv\Scripts\activate
# macOS/Linux:
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Run app locally
python -m flask run

# Or directly:
python app/app.py
```

## 2. Deploy to Vercel

### Option A: Using CLI
```bash
# Install Vercel CLI (if not already installed)
npm install -g vercel

# Login to Vercel
vercel login

# Deploy
vercel --prod
```

### Option B: Using GitHub Integration (Recommended)
1. Push code to GitHub: `git push origin main`
2. Go to https://vercel.com/dashboard
3. Click "Add New Project"
4. Import your GitHub repository
5. Project settings should auto-detect: Framework: Flask
6. Click "Deploy"

### Option C: Using Vercel Web UI
1. Go to https://vercel.com
2. Click "New Project"
3. Connect GitHub account
4. Select repository
5. Framework: Flask (auto-detected)
6. Deploy button

## 3. Environment Variables (Set in Vercel Dashboard)
Project Settings → Environment Variables:
```
FLASK_APP=api/index.py
FLASK_ENV=production
PYTHONUNBUFFERED=1
```

## 4. Verify Deployment
After deployment, test these URLs:
- `https://your-vercel-domain.vercel.app/` - Home
- `https://your-vercel-domain.vercel.app/about` - About
- `https://your-vercel-domain.vercel.app/dashboard` - Dashboard
- `https://your-vercel-domain.vercel.app/story` - Story
- `https://your-vercel-domain.vercel.app/contact` - Contact
- `https://your-vercel-domain.vercel.app/get_started` - Prediction Form

## 5. Troubleshooting

### Build Error: "No module named 'app'"
**Solution:** Ensure `api/index.py` properly imports from app
- Check: `sys.path.insert(0, str(Path(__file__).parent.parent))`

### Error: "Static files not found"
**Solution:** Use Flask's `url_for()` function in templates
- ✅ Correct: `{{ url_for('static', filename='css/base.css') }}`
- ❌ Wrong: `<link rel="stylesheet" href="/css/base.css">`

### Port Issues
**Solution:** Use environment variable for port
- Code: `port = int(os.environ.get('PORT', 5000))`

### CSS not loading in production
**Solution:** Check CSS in base.css is valid
- ✅ Already fixed: Changed `graytint()` to `rgba()`

## 6. Monitor Deployment

### Vercel Dashboard
- Watch build logs in real-time
- Check function execution
- Monitor serverless function duration
- View environment variables

### View Logs
```bash
# Real-time logs
vercel logs --prod

# Past deployments
vercel list
```

---
**Ready to deploy! Push your code and Vercel will handle the rest.** 🚀
