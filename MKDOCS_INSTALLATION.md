# MkDocs Material Installation Guide for Ubuntu Server

## Prerequisites
- Fresh Ubuntu server with SSH access
- sudo privileges

## Step 1: Update System & Install Python

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install python3 python3-pip python3-venv -y
```

## Step 2: Create Project Directory

```bash
mkdir -p ~/knowledge-base
cd ~/knowledge-base
```

## Step 3: Create Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate
```

## Step 4: Install MkDocs Material

```bash
pip install mkdocs-material
```

## Step 5: Create MkDocs Project

```bash
mkdocs new .
```

This creates:
- `mkdocs.yml` - Configuration file
- `docs/` - Documentation folder

## Step 6: Configure MkDocs

Edit `mkdocs.yml`:

```bash
nano mkdocs.yml
```

Replace contents with:

```yaml
site_name: Engineering Knowledge Base
site_description: Technical documentation and knowledge repository

theme:
  name: material
  palette:
    - scheme: default
      primary: indigo
      accent: indigo
      toggle:
        icon: material/brightness-7
        name: Switch to dark mode
    - scheme: slate
      primary: indigo
      accent: indigo
      toggle:
        icon: material/brightness-4
        name: Switch to light mode
  features:
    - navigation.tabs
    - navigation.sections
    - navigation.expand
    - navigation.top
    - search.suggest
    - search.highlight
    - content.code.copy

markdown_extensions:
  - pymdownx.highlight
  - pymdownx.superfences
  - pymdownx.tabbed
  - admonition
  - tables
```

## Step 7: Copy Your Knowledge Base Files

Transfer your knowledge base from Windows to the server:

```bash
# On your Windows machine, use SCP or WinSCP to copy files
# Or use this command in PowerShell:
scp -r "C:\Users\TierneyMorris\Documents\obsidian\KnowledgeBase\Engineering\*" user@server-ip:~/knowledge-base/docs/
```

Or manually copy the `Products/` and `Clients/` folders into `~/knowledge-base/docs/`

## Step 8: Test Locally

```bash
cd ~/knowledge-base
source venv/bin/activate
mkdocs serve -a 0.0.0.0:8000
```

Visit: `http://your-server-ip:8000`

## Step 9: Build Static Site

```bash
mkdocs build
```

This creates a `site/` folder with static HTML files.

## Step 10: Production Deployment with Nginx

### Install Nginx

```bash
sudo apt install nginx -y
```

### Configure Nginx

```bash
sudo nano /etc/nginx/sites-available/knowledge-base
```

Add:

```nginx
server {
    listen 80;
    server_name your-domain.com;  # or server IP
    
    root /home/your-username/knowledge-base/site;
    index index.html;
    
    location / {
        try_files $uri $uri/ =404;
    }
}
```

### Enable Site

```bash
sudo ln -s /etc/nginx/sites-available/knowledge-base /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl restart nginx
```

## Step 11: Auto-rebuild on Changes (Optional)

Create a systemd service to run MkDocs in serve mode:

```bash
sudo nano /etc/systemd/system/mkdocs.service
```

Add:

```ini
[Unit]
Description=MkDocs Material Server
After=network.target

[Service]
Type=simple
User=your-username
WorkingDirectory=/home/your-username/knowledge-base
ExecStart=/home/your-username/knowledge-base/venv/bin/mkdocs serve -a 0.0.0.0:8000
Restart=always

[Install]
WantedBy=multi-user.target
```

Enable and start:

```bash
sudo systemctl enable mkdocs
sudo systemctl start mkdocs
sudo systemctl status mkdocs
```

## Quick Reference

```bash
# Activate virtual environment
source ~/knowledge-base/venv/bin/activate

# Serve locally (development)
mkdocs serve

# Build static site
mkdocs build

# Deploy to GitHub Pages (if using)
mkdocs gh-deploy
```

## Done!

Your knowledge base is now live and searchable with a beautiful Material Design interface!

