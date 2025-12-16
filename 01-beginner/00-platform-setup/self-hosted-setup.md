# Self-Hosted Setup: Free n8n Community Edition

## Run n8n on Your Own VPS - Completely Free

This guide gets you running **n8n Community Edition** (free, open-source) on a Linux VPS using Docker in **15 minutes**.

---

## ✅ What You'll Get

- ✅ n8n running on your VPS
- ✅ Unlimited workflows
- ✅ Unlimited executions
- ✅ Complete data control
- ✅ Ready for production
- ✅ Zero licensing cost

---

## 📋 Prerequisites

You need:
1. **A Linux VPS** ($5-10/month or free tier)
   - Ubuntu 20.04 or later recommended
   - At least 1GB RAM, 1 vCPU
   - SSH access to the server

2. **Docker installed** (we'll help you install it)

3. **Basic Linux knowledge**
   - Can SSH into a server
   - Can run commands in terminal
   - Can edit files (nano or vim)

---

## 🎯 Free VPS Options

**Pick one if you don't have a VPS:**

| Provider | Price | Notes |
|----------|-------|-------|
| DigitalOcean | $5/mo | Easy setup, great docs |
| Linode | $5/mo | Reliable, good support |
| Vultr | $6/mo | Globally distributed |
| Hetzner | €4/mo | Europe-based, cheap |
| AWS EC2 | Free 1yr | Free tier, then $0.01/hr |
| Oracle Cloud | Free | 4GB RAM free tier (generous!) |

**Recommendation for beginners:** DigitalOcean (easiest to use)

---

## 🚀 Step-by-Step Setup (15 minutes)

### Step 1: SSH Into Your VPS (2 min)

```bash
# Replace YOUR_VPS_IP with your actual IP
ssh root@YOUR_VPS_IP

# You'll be prompted for password or key
# Once connected, you should see a prompt like: root@ubuntu:~#
```

### Step 2: Update System (2 min)

```bash
# Update package lists
apt-get update

# Upgrade packages (optional but recommended)
apt-get upgrade -y
```

### Step 3: Install Docker (3 min)

```bash
# Install Docker from official repo
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh

# Verify installation
docker --version
# Should show: Docker version 20.x.x (or newer)
```

### Step 4: Create Directory for n8n (1 min)

```bash
# Create folder to store n8n data
mkdir -p /opt/n8n
cd /opt/n8n

# Create directories for persistence
mkdir -p data
mkdir -p .n8n
```

### Step 5: Create docker-compose.yml (2 min)

```bash
# Create the docker compose file
nano docker-compose.yml
```

**Paste this content:**

```yaml
version: '3.8'

services:
  n8n:
    image: n8nio/n8n:latest
    container_name: n8n
    restart: unless-stopped
    
    environment:
      - N8N_HOST=YOUR_VPS_IP_OR_DOMAIN
      - N8N_PORT=5678
      - N8N_PROTOCOL=http
      - N8N_ENCRYPTION_KEY=your-secure-random-key-here-change-this-32chars
      - NODE_ENV=production
      - WEBHOOK_URL=http://YOUR_VPS_IP_OR_DOMAIN:5678/
      - GENERIC_TIMEZONE=UTC
    
    ports:
      - "5678:5678"
    
    volumes:
      - ./data:/home/node/.n8n
      - ./data:/root/.n8n
    
    networks:
      - n8n-network

networks:
  n8n-network:
    driver: bridge
```

**Important:** Replace `YOUR_VPS_IP_OR_DOMAIN` with your actual VPS IP or domain

**To save in nano:**
- Press `Ctrl + O`, then `Enter`
- Press `Ctrl + X` to exit

### Step 6: Generate Secure Encryption Key (1 min)

```bash
# Generate a random 32-character encryption key
head -c 32 /dev/urandom | base64

# Copy the output and replace N8N_ENCRYPTION_KEY in docker-compose.yml
```

### Step 7: Start n8n with Docker (2 min)

```bash
# Start n8n in the background
docker-compose up -d

# Watch the logs (takes 1-2 minutes to start)
docker-compose logs -f

# You should see:
# "n8n started" when ready
# Press Ctrl+C to exit logs
```

### Step 8: Verify n8n is Running (1 min)

```bash
# Check if container is running
docker ps

# Should show: n8nio/n8n running

# Or test with curl
curl http://localhost:5678
# Should get HTML response
```

---

## ✅ Access Your n8n

### From the Server:
```
http://YOUR_VPS_IP:5678
```

### From Your Computer:
1. Open browser
2. Go to `http://YOUR_VPS_IP:5678`
3. Create admin account on first login
4. Set username and password
5. You're in! 🎉

---

## 🔐 Security: Important Steps

### Enable HTTPS (Recommended for Production)

If you have a domain, use Let's Encrypt:

```bash
# Install Certbot
apt-get install certbot python3-certbot-nginx -y

# Get certificate
certbot certonly --standalone -d yourdomain.com

# Update docker-compose.yml to use HTTPS
# Change N8N_PROTOCOL from http to https
# Add SSL certificate paths to volumes
```

### Firewall Rules

```bash
# Allow SSH
ufw allow 22/tcp

# Allow n8n
ufw allow 5678/tcp

# Allow HTTPS (if using)
ufw allow 443/tcp

# Enable firewall
ufw enable
```

### Strong Admin Password

When you first access n8n:
- Use a **strong, unique password** (20+ characters)
- Use password manager to store it
- Don't share it

---

## 🆘 Troubleshooting

### Issue: Port 5678 already in use
```bash
# Find what's using port 5678
lsof -i :5678

# Or use different port in docker-compose.yml
# Change ports: "5678:5678" to "8080:5678"
```

### Issue: Docker not found
```bash
# Reinstall Docker
curl -fsSL https://get.docker.com | sh

# Add user to docker group (optional)
usermod -aG docker $USER
```

### Issue: n8n not starting
```bash
# Check logs for errors
docker-compose logs

# Restart the container
docker-compose restart

# Rebuild if needed
docker-compose down
docker-compose up -d
```

### Issue: Can't connect from outside server
```bash
# Check firewall
ufw status

# Check if port is listening
netstat -tuln | grep 5678

# Restart n8n
docker-compose restart
```

---

## 🚀 Useful Docker Commands

```bash
# Start n8n
docker-compose up -d

# Stop n8n
docker-compose down

# Restart n8n
docker-compose restart

# View logs
docker-compose logs -f

# Update to latest n8n
docker-compose pull
docker-compose up -d

# Backup your data
tar -czf n8n-backup.tar.gz data/

# Restore from backup
tar -xzf n8n-backup.tar.gz
docker-compose up -d
```

---

## 📊 Verification Checklist

- [ ] VPS is accessible via SSH
- [ ] Docker is installed (`docker --version` works)
- [ ] Directory `/opt/n8n` created
- [ ] `docker-compose.yml` file created
- [ ] Encryption key generated and added
- [ ] n8n container is running (`docker ps` shows n8n)
- [ ] Can access n8n in browser
- [ ] Created admin account
- [ ] Can log in successfully

---

## 💾 Backup Your Data

Important: Back up your n8n data regularly!

```bash
# Backup command
tar -czf n8n-backup-$(date +%Y%m%d).tar.gz data/

# Restore command
tar -xzf n8n-backup-20251216.tar.gz
docker-compose restart
```

**Store backups in:** 
- Cloud storage (Google Drive, AWS S3, etc.)
- Another server
- Encrypted USB drive

---

## 🔄 Updates

n8n is actively developed. Update regularly:

```bash
# Check for updates
docker pull n8nio/n8n:latest

# Update and restart
docker-compose pull
docker-compose up -d

# Verify update
docker-compose logs | grep "n8n started"
```

---

## 📝 Configuration Options

You can customize n8n via environment variables in `docker-compose.yml`:

```yaml
# Database (default: SQLite, stored in data/)
DB_TYPE=sqlite
# DB_TYPE=postgres  # for PostgreSQL

# Email (for notifications)
# MAIL_HOST=smtp.gmail.com
# MAIL_PORT=587
# MAIL_USERNAME=your-email@gmail.com
# MAIL_PASSWORD=your-app-password

# Timezone
GENERIC_TIMEZONE=America/New_York

# Workflow execution concurrency
N8N_EXECUTION_MODE=queue
```

See [n8n docs](https://docs.n8n.io/) for all options.

---

## 🎯 Next Steps

### After Setup:
1. ✅ Access n8n in browser
2. ✅ Create admin account
3. ✅ Read credentials guide (security important!)
4. ✅ Test by creating hello-world workflow
5. ✅ Ready to start learning!

### Coming Next:
- Learn core concepts (nodes, triggers, workflows)
- Create your first workflow
- Understand data flow
- Start building automations

---

## 💡 Tips

**Tip 1: Monitor Resources**
```bash
# Check CPU/memory usage
docker stats n8n
```

**Tip 2: Enable Auto-Restarts**
The `restart: unless-stopped` in docker-compose handles this

**Tip 3: Scale Up Later**
If you need more resources:
- Increase VPS RAM/CPU
- Switch to PostgreSQL for larger databases
- Use separate queue workers for execution

**Tip 4: Use a Domain**
Instead of IP, use a domain:
- Makes sharing easier
- Required for proper HTTPS
- Recommended for production

---

## 🔗 Resources

- [n8n Official Docs](https://docs.n8n.io/)
- [n8n Community Forum](https://community.n8n.io/)
- [Docker Documentation](https://docs.docker.com/)
- [Docker Compose Reference](https://docs.docker.com/compose/compose-file/)

---

## ✨ You're Done!

Your n8n instance is running on your VPS! 🎉

### What You Have:
✅ n8n running 24/7 on your VPS  
✅ Data stored on your server  
✅ Unlimited workflows  
✅ Unlimited executions  
✅ Complete control  
✅ Zero cost  

### Next:
👉 Read `credentials-guide.md` (how to securely store API keys)

---

**Last Updated:** December 2025  
**Status:** Self-Hosted Setup Complete  
**Next:** Credentials Management & Security

Good luck! 🚀
