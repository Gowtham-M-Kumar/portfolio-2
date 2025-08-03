# Deployment Checklist for Render

## ✅ Pre-Deployment Checklist

### 1. Code Preparation
- [x] All code is committed to GitHub
- [x] `requirements.txt` is up to date
- [x] `build.sh` script is executable and correct
- [x] Django settings are production-ready
- [x] Static files are properly configured
- [x] Database migrations are ready

### 2. Environment Variables
- [ ] Generate a secure `SECRET_KEY`
- [ ] Set `DEBUG=False`
- [ ] Configure `ALLOWED_HOSTS` for your domain
- [ ] Set up email configuration (optional)

### 3. Database
- [x] PostgreSQL database is created on Render
- [x] Database migrations are tested
- [x] Data has been migrated from SQLite to PostgreSQL

## 🚀 Render Deployment Steps

### Step 1: Create Web Service
1. Go to [Render Dashboard](https://dashboard.render.com)
2. Click "New +" → "Web Service"
3. Connect your GitHub repository

### Step 2: Configure Service
- **Name**: `portfolio-project` (or your preferred name)
- **Environment**: `Python 3`
- **Region**: Choose closest to your users
- **Branch**: `main` (or your default branch)
- **Root Directory**: `portfolio_project` (if Django project is in subdirectory)
- **Build Command**: `./build.sh`
- **Start Command**: `gunicorn portfolio_project.wsgi:application`

### Step 3: Environment Variables
Add these in Render's environment variables section:

```
SECRET_KEY=your-secure-secret-key-here
DEBUG=False
ALLOWED_HOSTS=your-app-name.onrender.com
```

### Step 4: Database Connection
- Create a new PostgreSQL database in Render
- Render will automatically provide `DATABASE_URL`
- Link the database to your web service

### Step 5: Deploy
- Click "Create Web Service"
- Monitor the build logs
- Wait for deployment to complete

## 🔧 Post-Deployment

### 1. Verify Deployment
- [ ] Website loads correctly
- [ ] Admin panel is accessible
- [ ] Static files are loading
- [ ] Database is working
- [ ] Contact form functions

### 2. Security
- [ ] HTTPS is enabled
- [ ] Admin panel is secure
- [ ] Environment variables are set
- [ ] Debug mode is disabled

### 3. Content Setup
- [ ] Create admin superuser
- [ ] Add your projects
- [ ] Configure resume sections
- [ ] Test contact form

## 🛠️ Troubleshooting

### Common Issues

1. **Build Fails**
   - Check build logs in Render dashboard
   - Verify `requirements.txt` is correct
   - Ensure `build.sh` is executable

2. **Static Files Not Loading**
   - Verify WhiteNoise is configured
   - Check `STATIC_ROOT` and `STATIC_URL` settings
   - Ensure `collectstatic` runs in build script

3. **Database Connection Errors**
   - Verify `DATABASE_URL` is set
   - Check PostgreSQL service is running
   - Ensure migrations are applied

4. **500 Server Errors**
   - Check application logs in Render
   - Verify all environment variables are set
   - Check Django settings for production

### Useful Commands

```bash
# Generate secure secret key
python -c "from django.core.management.utils import get_random_secret_key; print(get_random_secret_key())"

# Test local production settings
python manage.py check --deploy

# Collect static files locally
python manage.py collectstatic --no-input

# Test database connection
python manage.py dbshell
```

## 📞 Support

If you encounter issues:
1. Check Render logs in the dashboard
2. Review Django error logs
3. Verify environment variables
4. Test database connection
5. Check static file configuration

## 🎉 Success!

Once deployed successfully, your portfolio will be available at:
`https://your-app-name.onrender.com`

Remember to:
- Update your resume with the new URL
- Share the link on your social profiles
- Monitor the site for any issues
- Keep the code updated and secure 