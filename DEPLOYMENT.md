# Deployment Guide for Car Price Predictor

## Quick Start - Streamlit Cloud (Easiest ⭐)

1. **Sign up for free at**: https://share.streamlit.io/

2. **Connect your GitHub account**

3. **Click "New app"** and select:
   - Repository: `munna44sagarpal-collab/car-price-predictor`
   - Branch: `main`
   - Main file path: `app.py`

4. **Click "Deploy"** - Your app will be live in minutes!

Your app will be available at: `https://share.streamlit.io/munna44sagarpal-collab/car-price-predictor/main/app.py`

---

## Alternative Deployment Options

### Heroku Deployment

1. **Prerequisites**:
   - Heroku account (free tier available)
   - Heroku CLI installed

2. **Steps**:
   ```bash
   # Login to Heroku
   heroku login
   
   # Create a new app
   heroku create your-unique-app-name
   
   # Deploy
   git push heroku main
   
   # View your app
   heroku open
   ```

3. **Monitor logs**:
   ```bash
   heroku logs --tail
   ```

### Docker Deployment (AWS, Google Cloud, Azure)

**Dockerfile** (already includes in repo):
```dockerfile
FROM python:3.10-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
CMD ["streamlit", "run", "app.py", "--server.port=8501", "--server.address=0.0.0.0"]
```

**Build and Run**:
```bash
docker build -t car-price-predictor .
docker run -p 8501:8501 car-price-predictor
```

### PythonAnywhere (Easy for Beginners)

1. Create account at https://www.pythonanywhere.com/
2. Upload your files
3. Configure web app settings
4. Done!

### Render.com (Free Alternative to Heroku)

1. Push to GitHub
2. Go to https://render.com/
3. Click "Create Web Service"
4. Connect your GitHub repo
5. Select `main` branch and `app.py` as entry command
6. Deploy!

---

## Post-Deployment Checklist

- [ ] App loads without errors
- [ ] Can select company, model, year, fuel type
- [ ] Prediction works correctly
- [ ] Input validation works
- [ ] Error handling displays appropriately

## Troubleshooting

### App crashes after deployment
- Check logs: `streamlit logs`
- Verify all required files exist in `models/` and `data/` directories
- Check Python version compatibility

### Model file not found
- Ensure `models/LinearRegressionModel.pkl` is committed to Git
- Check file paths in `app.py`

### Data file not found
- Ensure `data/Cleaned_Car_data.csv` is committed to Git
- Verify file encoding (UTF-8 recommended)

### Slow predictions
- Streamlit caches the model with `@st.cache_resource`
- First load may be slower, subsequent requests are instant

---

## Environment Variables (Optional)

For storing sensitive data, create `.streamlit/secrets.toml`:
```toml
# .streamlit/secrets.toml
api_key = "your-api-key-here"
```

Access in app:
```python
import streamlit as st
api_key = st.secrets["api_key"]
```

---

## Cost Analysis

| Platform | Cost | Best For |
|----------|------|----------|
| **Streamlit Cloud** | Free | Quick deployment, hobby projects |
| **Heroku** | $7/month | Small apps, learning |
| **Render.com** | Free tier available | Reliable, easy setup |
| **AWS/GCP/Azure** | Pay-per-use | Production, scaling |

---

For more help, visit:
- https://docs.streamlit.io/streamlit-community-cloud
- https://devcenter.heroku.com/articles/deploying-python-apps-on-heroku
