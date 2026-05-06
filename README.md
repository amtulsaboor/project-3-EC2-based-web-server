 #  Project 3: EC2-Based Web Server Deployment (Apache/Nginx on AWS)

This project demonstrates how to deploy a web server on an Amazon EC2 instance by launching a virtual machine, configuring security groups, installing either **Apache (httpd)** or **Nginx**, and hosting a simple web page.

This is a beginner-friendly AWS + Linux + Web Server project commonly used in real-world hosting environments.

---

## 📌 Project Overview

In this project, you will:

- Launch an EC2 instance on AWS
- Connect to the instance using SSH
- Install Apache or Nginx
- Configure firewall/security groups
- Deploy a sample web page
- Access the website using EC2 Public IP
- Enable auto-start for the web server

---

# 🏗️ Architecture

```bash
User Browser → Internet → AWS Security Group → EC2 Instance → Apache/Nginx → Website
````

---

# 🛠️ Services Used

* **AWS EC2**
* **AWS Security Groups**
* **Amazon Linux / Ubuntu**
* **Apache (httpd)** OR **Nginx**
* **SSH**
* **Linux Commands**

---

# Step 1: Launch EC2 Instance

Login to AWS Console:

➡ Open AWS Console
➡ Navigate to EC2 Dashboard
➡ Click **Launch Instance**

### Configure Instance:

| Setting        | Value                      |
| -------------- | -------------------------- |
| Name           | MyWebServer                |
| AMI            | Amazon Linux 2 / Ubuntu    |
| Instance Type  | t2.micro                   |
| Key Pair       | Create new/existing        |
| Security Group | Allow SSH (22) + HTTP (80) |

Click **Launch Instance**

---
<img width="1710" height="1107" alt="Screenshot 2026-05-04 at 9 07 12 PM" src="https://github.com/user-attachments/assets/85832a51-a894-449c-b0ca-9795baeb7519" />



---

# Step 2: Connect to EC2 Instance

Use SSH to connect:

### For Amazon Linux

```bash
ssh -i your-key.pem ec2-user@your-public-ip
```

### For Ubuntu

```bash
ssh -i your-key.pem ubuntu@your-public-ip
```

---

## Verify Connection

```bash
whoami
```

Expected output:

```bash
ec2-user
```

or

```bash
ubuntu
```

---

# Step 3: Update System Packages

### Amazon Linux

```bash
sudo yum update -y
```

### Ubuntu

```bash
sudo apt update -y
```

---

# Step 4: Install Apache Web Server

## Amazon Linux

```bash
sudo yum install httpd -y
```

## Ubuntu

```bash
sudo apt install apache2 -y
```

---

# Step 5: Start Apache Service

## Amazon Linux

```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```

## Ubuntu

```bash
sudo systemctl start apache2
sudo systemctl enable apache2
```

---

# Step 6: Verify Apache Status

### Amazon Linux

```bash
sudo systemctl status httpd
```

### Ubuntu

```bash
sudo systemctl status apache2
```

Expected output:

```bash
active (running)
```
<img width="1710" height="1107" alt="Screenshot 2026-05-04 at 9 31 20 PM" src="https://github.com/user-attachments/assets/76643b8c-d55e-4251-a091-f2f18c562eb4" />


**
---

# Alternative: Install Nginx

If you prefer Nginx instead of Apache:

## Amazon Linux

```bash
sudo yum install nginx -y
```

## Ubuntu

```bash
sudo apt install nginx -y
```

Start service:

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

Check status:

```bash
sudo systemctl status nginx
```

---

# Step 7: Configure Firewall

### For Amazon Linux

Allow HTTP traffic:

```bash
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --reload
```

> Note: If your EC2 Security Group already allows port 80, this step may not be necessary.

---

# Step 8: Deploy Sample Website

### Apache Default Path

```bash
sudo echo "<h1>Welcome to My Web Server</h1>" > /var/www/html/index.html
```

### Nginx Default Path

```bash
sudo echo "<h1>Welcome to My Web Server</h1>" > /usr/share/nginx/html/index.html
```

---

# Step 9: Access Website

Copy your EC2 Public IP and open:

```bash
http://your-public-ip
```

You should see:

```bash
Welcome to My Web Server
```
<img width="1710" height="1107" alt="Screenshot 2026-05-04 at 9 49 54 PM" src="https://github.com/user-attachments/assets/181afb85-4c2c-4c98-af34-f00502bd09be" />


---

# Step 10: Verify Auto Start on Reboot

### Apache

```bash
sudo systemctl enable httpd
```

### Nginx

```bash
sudo systemctl enable nginx
```

---

# Useful Commands

Check running services:

```bash
sudo systemctl list-units --type=service
```

Check open ports:

```bash
sudo netstat -tulnp
```

Check web server logs:

### Apache

```bash
sudo tail -f /var/log/httpd/access_log
```

### Nginx

```bash
sudo tail -f /var/log/nginx/access.log
```

---

# Common Errors & Fixes

## Permission Denied While SSH

```bash
chmod 400 your-key.pem
```

---

## Website Not Loading

Check:

* Security Group allows port 80
* Web server service is running
* Firewall rules configured properly

---

## Apache Port Issue

Check Apache port configuration:

```bash
sudo cat /etc/httpd/conf/httpd.conf
```

Default port:

```bash
Listen 80
```

---

# Project Outcome

✅ EC2 launched successfully
✅ Web server installed
✅ Website hosted
✅ Security configured
✅ Auto-start enabled

---

# Real-World Use Cases

* Website hosting
* Reverse proxy setup
* Hosting internal applications
* Learning Linux administration
* DevOps beginner project

---

# Folder Structure

```bash
EC2-Web-Server/
│
├── screenshots/
├── README.md
└── sample-website/
```

---

# Author

**Amtul Saboor**
DevOps & Cloud Engineer

