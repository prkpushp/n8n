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

