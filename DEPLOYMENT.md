# Icon Manager Deployment Guide

## Quick Deploy Options

### Option 1: Vercel (Frontend) + Railway (Backend) - Recommended

#### Backend Deployment (Railway)

1. **Sign up for Railway** at https://railway.app
2. **Connect your GitHub repository**
3. **Create a new project** and select your repository
4. **Set environment variables:**
   - `PORT`: Railway will set this automatically
5. **Deploy** - Railway will automatically detect it's a Python app
6. **Get your backend URL** (e.g., `https://your-app.railway.app`)

#### Frontend Deployment (Vercel)

1. **Sign up for Vercel** at https://vercel.com
2. **Import your GitHub repository**
3. **Configure the project:**
   - Framework Preset: Vite
   - Root Directory: `frontend`
   - Build Command: `npm run build`
   - Output Directory: `dist`
4. **Set environment variables:**
   - `VITE_BACKEND_URL`: Your Railway backend URL
5. **Deploy**

### Option 2: Netlify (Frontend) + Render (Backend)

#### Backend Deployment (Render)

1. **Sign up for Render** at https://render.com
2. **Create a new Web Service**
3. **Connect your GitHub repository**
4. **Configure:**
   - Name: `icon-manager-backend`
   - Environment: Python 3
   - Build Command: `pip install -r requirements.txt`
   - Start Command: `cd backend && uvicorn main:app --host 0.0.0.0 --port $PORT`
5. **Deploy**

#### Frontend Deployment (Netlify)

1. **Sign up for Netlify** at https://netlify.com
2. **Import your GitHub repository**
3. **Configure:**
   - Base directory: `frontend`
   - Build command: `npm run build`
   - Publish directory: `dist`
4. **Set environment variables:**
   - `VITE_BACKEND_URL`: Your Render backend URL
5. **Deploy**

### Option 3: Heroku (Full Stack)

1. **Install Heroku CLI**
2. **Login to Heroku:**
   ```bash
   heroku login
   ```
3. **Create Heroku app:**
   ```bash
   heroku create your-icon-manager
   ```
4. **Set buildpacks:**
   ```bash
   heroku buildpacks:clear
   heroku buildpacks:add heroku/nodejs
   heroku buildpacks:add heroku/python
   ```
5. **Deploy:**
   ```bash
   git push heroku main
   ```

## Environment Variables

### Backend
- `PORT`: Set automatically by hosting platform
- `CORS_ORIGINS`: Your frontend URL (optional)

### Frontend
- `VITE_BACKEND_URL`: Your backend URL

## File Structure for Deployment

```
icon_project/
├── backend/
│   ├── main.py
│   └── icons/
├── frontend/
│   ├── src/
│   ├── package.json
│   └── vite.config.js
├── exported_svgs/
├── flags/
├── requirements.txt
├── Procfile
├── runtime.txt
└── README.md
```

## Troubleshooting

### Common Issues

1. **CORS Errors**: Make sure your backend allows your frontend domain
2. **Build Failures**: Check that all dependencies are in requirements.txt
3. **Port Issues**: Use `$PORT` environment variable in production
4. **File Paths**: Ensure relative paths work in production

### Local Testing

1. **Test backend:**
   ```bash
   cd backend
   python main.py
   ```

2. **Test frontend:**
   ```bash
   cd frontend
   npm run dev
   ```

## Cost Estimates

- **Vercel**: Free tier (frontend)
- **Railway**: $5/month (backend)
- **Render**: Free tier available
- **Netlify**: Free tier (frontend)
- **Heroku**: $7/month (basic dyno)

## Security Considerations

1. **Environment Variables**: Never commit sensitive data
2. **CORS**: Configure properly for production
3. **File Uploads**: Consider file size limits
4. **Rate Limiting**: Implement if needed

## Monitoring

- Set up logging for your backend
- Monitor application performance
- Set up alerts for downtime 