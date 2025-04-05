# Deployment Guide for GitHub Pages

## Prerequisites
- A GitHub account
- Git installed on your local machine
- Python 3.8 or higher installed
- pip (Python package manager) installed

## Step 1: Prepare Your Repository
1. Create a new repository on GitHub named `yourusername.github.io`
2. Clone the repository to your local machine:
   ```bash
   git clone https://github.com/yourusername/yourusername.github.io.git
   cd yourusername.github.io
   ```

## Step 2: Set Up Your Project
1. Create and activate a virtual environment:
   ```bash
   python -m venv venv
   # On Windows
   venv\Scripts\activate
   # On macOS/Linux
   source venv/bin/activate
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Configure your Django settings:
   - Create a `.env` file in your project root
   - Add the following environment variables:
     ```
     DEBUG=False
     ALLOWED_HOSTS=yourusername.github.io
     SECRET_KEY=your-secret-key
     ```

## Step 3: Deploy to GitHub Pages
1. Build your static files:
   ```bash
   python manage.py collectstatic
   ```

2. Add and commit your changes:
   ```bash
   git add .
   git commit -m "Initial deployment"
   ```

3. Push to GitHub:
   ```bash
   git push origin main
   ```

4. Go to your repository settings on GitHub:
   - Navigate to "Settings" > "Pages"
   - Under "Source", select "main" branch
   - Click "Save"

## Step 4: Configure GitHub Actions (Optional)
Create a `.github/workflows/deploy.yml` file:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.8'
    
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    
    - name: Collect static files
      run: python manage.py collectstatic --noinput
    
    - name: Deploy to GitHub Pages
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./staticfiles
```

## Step 5: Verify Deployment
1. Wait a few minutes for GitHub Pages to build your site
2. Visit `https://yourusername.github.io` to verify your portfolio is live

## Troubleshooting
- If your site doesn't appear, check GitHub Actions for any build errors
- Ensure all static files are being collected properly
- Verify your repository settings and permissions
- Check that your domain settings are correct in Django settings

## Maintenance
- To update your portfolio, make changes locally and push to GitHub
- GitHub Actions will automatically deploy updates
- Monitor your GitHub repository for any deployment issues

## Additional Resources
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Django Deployment Checklist](https://docs.djangoproject.com/en/4.2/howto/deployment/checklist/)
- [GitHub Actions Documentation](https://docs.github.com/en/actions) 