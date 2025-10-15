# Deploy Simple HTML/CSS Website on VPS (Ready-to-Use)

This guide shows how to deploy a static HTML/CSS website on a VPS using Nginx.

---

## 1️⃣ Connect to VPS

```bash
ssh root@your_server_ip
add pass

2️⃣ Update Server
bash
Copy code
sudo apt update && sudo apt upgrade -y

3️⃣ Install Nginx
bash
Copy code
sudo apt install nginx -y
sudo systemctl enable nginx
sudo systemctl start nginx
systemctl status nginx

4️⃣ Upload Website Files
Create folder:

bash
Copy code
sudo mkdir -p /var/www/mywebsite
Upload files (replace paths):

bash
Copy code
scp -r ./local-website-folder/* root@your_server_ip:/var/www/mywebsite
Set permissions:

bash
Copy code
sudo chown -R www-data:www-data /var/www/mywebsite
sudo chmod -R 755 /var/www/mywebsite


5️⃣ Configure Nginx
Create site config:

bash
Copy code
sudo nano /etc/nginx/sites-available/mywebsite
Paste:

nginx
Copy code
server {
    listen 80;
    server_name yourdomain.com www.yourdomain.com;

    root /var/www/mywebsite;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
Enable site & reload:

bash
Copy code
sudo ln -s /etc/nginx/sites-available/mywebsite /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx


6️⃣ (Optional) Point Domain
Add A Records in your DNS:

python
Copy code
@   → your_server_ip
www → your_server_ip


7️⃣ (Optional) Enable HTTPS
Install Certbot:

bash
Copy code
sudo apt install certbot python3-certbot-nginx -y
sudo certbot --nginx -d yourdomain.com -d www.yourdomain.com


8️⃣ Test Website
Visit:

arduino
Copy code
http://yourdomain.com
https://yourdomain.com
🔹 Bonus Commands
Reload Nginx after changes:

bash
Copy code
sudo systemctl reload nginx
Check logs:

bash
Copy code
tail -f /var/log/nginx/error.log
tail -f /var/log/nginx/access.log
🎉 Your static website is now live on your VPS!

yaml
Copy code

---

If you want, I can also **make a version with prefilled example domain and server IP**, so you literally just copy, paste, and it works immediately.  

Do you want me to do that?