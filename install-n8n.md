# Video Tutorial 
[![Install N8N on Linux/GCP/AWS/Oracle)


## Step 1: Install Docker
```bash
   sudo apt update
   sudo apt install docker.io
   sudo systemctl start docker
   sudo systemctl enable docker
```

## Step 2: Starting n8n in Docker
** Replace n8n.cloudblog.fun with your actual domain name/subdomain:**
```bash
    sudo docker run -d --restart unless-stopped -it \
    --name n8n \
    -p 5678:5678 \
    -e N8N_HOST="n8n.cloudblog.fun" \
    -e WEBHOOK_TUNNEL_URL="https://n8n.cloudblog.fun/" \
    -e WEBHOOK_URL="https://n8n.cloudblog.fun/" \
    -v ~/.n8n:/root/.n8n \
    n8nio/n8n
```
## Step 3: Installing Nginx (used as a reverse proxy to n8n and handle SSL termination)

```bash
   sudo apt install nginx
   sudo vi /etc/nginx/sites-available/n8n.conf
```
   **Paste the Following data: Replace your domain/subdomain n8n.cloudblog.fun**
```bash
    server {
        listen 80;
        server_name n8n.cloudblog.fun

        location / {
        proxy_pass http://localhost:5678;
        proxy_http_version 1.1;
        chunked_transfer_encoding off;
        proxy_buffering off;
        proxy_cache off;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto https;
        proxy_read_timeout 86400;
        }
    }
```
    **Enable and restart:**
    ```bash
    sudo ln -s /etc/nginx/sites-available/n8n.conf /etc/nginx/sites-enabled/
    sudo nginx -t
    sudo systemctl restart nginx

## Step 4: Setting up SSL with Certbot
```bash
   sudo apt install certbot python3-certbot-nginx
   sudo certbot --nginx -d n8n.cloudblog.fun
```
