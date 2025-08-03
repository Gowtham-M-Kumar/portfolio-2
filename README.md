# Portfolio Project

A Django-based portfolio website with project showcase, resume management, and contact functionality.

## Features

- **Portfolio Showcase**: Display your projects with images, descriptions, and links
- **Resume Management**: Manage resume sections and content
- **Contact Form**: Allow visitors to send messages
- **Admin Panel**: Full Django admin interface for content management
- **Responsive Design**: Modern, mobile-friendly interface
- **PostgreSQL Database**: Production-ready database setup

## Tech Stack

- **Backend**: Django 5.2.4
- **Database**: PostgreSQL (production), SQLite (development)
- **Static Files**: WhiteNoise
- **Server**: Gunicorn
- **Deployment**: Render

## Local Development

### Prerequisites

- Python 3.8+
- pip

### Setup

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd portfolio_project
   ```

2. **Create virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables**
   ```bash
   cp env.example .env
   # Edit .env with your settings
   ```

5. **Run migrations**
   ```bash
   python manage.py migrate
   ```

6. **Create superuser**
   ```bash
   python manage.py createsuperuser
   ```

7. **Run development server**
   ```bash
   python manage.py runserver
   ```

8. **Access the application**
   - Main site: http://localhost:8000
   - Admin panel: http://localhost:8000/admin

## Deployment on Render

### Prerequisites

- Render account
- GitHub repository with your code

### Deployment Steps

1. **Connect to Render**
   - Log in to [Render](https://render.com)
   - Click "New +" and select "Web Service"
   - Connect your GitHub repository

2. **Configure the Web Service**
   - **Name**: `portfolio-project` (or your preferred name)
   - **Environment**: `Python 3`
   - **Build Command**: `./build.sh`
   - **Start Command**: `gunicorn portfolio_project.wsgi:application`
   - **Root Directory**: `portfolio_project` (if your Django project is in a subdirectory)

3. **Environment Variables**
   Set these in Render's environment variables section:
   ```
   SECRET_KEY=your-secure-secret-key-here
   DEBUG=False
   ALLOWED_HOSTS=your-app-name.onrender.com
   DATABASE_URL=postgresql://... (Render will provide this automatically)
   ```

4. **Database Setup**
   - Create a new PostgreSQL database in Render
   - Render will automatically provide the `DATABASE_URL`
   - The build script will run migrations automatically

5. **Deploy**
   - Click "Create Web Service"
   - Render will build and deploy your application
   - Your site will be available at `https://your-app-name.onrender.com`

### Environment Variables Reference

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| `SECRET_KEY` | Django secret key | Yes | - |
| `DEBUG` | Debug mode | No | False |
| `ALLOWED_HOSTS` | Allowed hostnames | No | localhost,127.0.0.1,.onrender.com |
| `DATABASE_URL` | Database connection | No | SQLite (development) |

## Project Structure

```
portfolio_project/
├── main/                 # Main app with portfolio content
├── projects/            # Project management
├── resume/              # Resume management
├── contact/             # Contact form handling
├── static/              # Static files (CSS, JS, images)
├── media/               # User uploaded files
├── portfolio_project/   # Django project settings
├── manage.py           # Django management script
├── requirements.txt    # Python dependencies
└── build.sh           # Render build script
```

## Admin Panel

Access the Django admin panel at `/admin` to manage:
- Projects
- Resume sections
- Contact messages
- User accounts
- Site content

## Customization

### Adding Projects
1. Go to Admin Panel → Projects
2. Add new project with:
   - Title
   - Description
   - Image
   - GitHub/Live links
   - Tags

### Managing Resume
1. Go to Admin Panel → Resume Sections
2. Add/edit resume content sections

### Contact Form
The contact form automatically saves messages to the database and can be configured to send emails.

## Troubleshooting

### Common Issues

1. **Static files not loading**
   - Ensure `python manage.py collectstatic` was run
   - Check WhiteNoise configuration

2. **Database connection errors**
   - Verify `DATABASE_URL` is set correctly
   - Check PostgreSQL service is running

3. **Migration errors**
   - Run `python manage.py migrate` manually
   - Check for conflicting migrations

### Support

For deployment issues, check:
- Render logs in the dashboard
- Django error logs
- Database connection status

## License

This project is open source and available under the [MIT License](LICENSE). 