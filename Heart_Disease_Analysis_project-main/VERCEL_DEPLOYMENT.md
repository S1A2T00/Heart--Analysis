# Vercel Deployment Guide

## Changes Made for Vercel Compatibility

### 1. **Fixed CSS Issues** ✅
   - Removed invalid `graytint()` CSS function from `base.css`
   - Replaced with valid CSS expression: `rgba(255, 255, 255, 0.98)`
   - All styling and visual appearance preserved

### 2. **Optimized Dependencies** ✅
   - Removed unnecessary packages (Streamlit, matplotlib, scipy, etc.)
   - Kept only essential packages for Flask app and ML predictions
   - Reduced build size and deployment time
   - **Updated packages:**
     - Flask==3.1.2
     - gunicorn==23.0.0
     - scikit-learn==1.8.0
     - pandas==2.3.3
     - numpy==2.4.2
     - joblib==1.5.3
     - requests==2.32.5
     - python-dotenv==1.0.0

### 3. **Production-Ready Configuration** ✅
   - Updated `app.py` to use environment variables for PORT and DEBUG mode
   - Created `vercel.json` with proper Flask configuration
   - Added Python runtime specification (`runtime.txt`)
   - Created `.env.example` for environment variables

### 4. **Vercel API Handler** ✅
   - Created `api/index.py` as WSGI entry point for Vercel
   - Properly configured Python path for module imports
   - Added `__init__.py` for API module

## Deployment Steps

### Local Testing
```bash
# Install dependencies
pip install -r requirements.txt

# Run locally
python app/app.py
```

### Deploy to Vercel
```bash
# Install Vercel CLI
npm install -g vercel

# Login to Vercel
vercel login

# Deploy
vercel --prod

# Or use GitHub integration for automatic deployments
```

## Environment Variables (Vercel Dashboard)
Set in Vercel Project Settings → Environment Variables:
- `FLASK_APP`: `api/index.py`
- `FLASK_ENV`: `production`
- `PYTHONUNBUFFERED`: `1`

## File Structure
```
.
├── api/
│   ├── __init__.py
│   └── index.py           (WSGI entry point)
├── app/
│   ├── __init__.py
│   ├── app.py            (Flask application)
│   ├── static/
│   │   ├── css/          (All styling files)
│   │   ├── js/           (JavaScript files)
│   │   └── images/
│   └── templates/        (HTML templates)
├── models/
│   ├── predict.py        (ML prediction logic)
│   └── train_model.py
├── data/                 (Dataset files)
├── Procfile              (For Heroku - keep for reference)
├── requirements.txt      (Optimized dependencies)
├── runtime.txt          (Python version)
├── vercel.json          (Vercel configuration)
└── .env.example         (Environment template)
```

## Functionality Preserved ✅
- ✅ All Flask routes working
- ✅ Static files (CSS, JS, images) serving correctly
- ✅ ML prediction functionality intact
- ✅ Data visualization dashboard links
- ✅ Form submissions and API endpoints
- ✅ All original styling maintained

## Troubleshooting

### Build fails with "gunicorn not found"
- Ensure `requirements.txt` is updated
- Vercel should automatically install from requirements.txt

### Static files not loading
- Check that `url_for('static', ...)` is used in templates ✓
- Vercel serves static files automatically from `/app/static`

### Port issues
- Vercel runs on port specified in environment or 5000 by default
- `app.py` now reads PORT from environment variable

## Next Steps
1. Push changes to GitHub
2. Connect repository to Vercel
3. Deploy via Vercel Dashboard or CLI
4. Monitor logs in Vercel Dashboard
