# AWS AMI (Amazon Machine Image) – Step by Step Guide

## 📌 Definition

**Amazon Machine Image (AMI)** ek pre-configured template hota hai jisme Operating System, installed software, application configuration aur permissions included hote hain. AMI ka use karke hum same configuration ke EC2 instances easily aur quickly launch kar sakte hain.

> **Simple words:**
> **AMI = EC2 instance ka ready-made image (OS + Software + Settings)**

---

## 📂 Types of AMI

### 1️⃣ Amazon Provided AMI

* AWS ke dwara provide ki jati hai
* Examples: Amazon Linux, Ubuntu, Windows

### 2️⃣ Marketplace AMI

* Third-party vendors ki AMI
* Examples: WordPress, Docker, MySQL pre-installed

### 3️⃣ Custom AMI

* User khud create karta hai
* Apne installed software aur configuration ke sath

👉 **Is project me Custom AMI use ki gayi hai**

---

## 🎯 Use Cases of AMI

* Production servers quickly deploy karna
* Auto Scaling ke liye same configuration reuse karna
* Backup aur disaster recovery
* Dev, Test aur Production environments same rakhna
* Multiple web servers with identical setup

---

## 🛠️ Practical: Create AMI & Launch Instance

### 🔹 Step 1: Existing EC2 Instance

> Is case me EC2 instance pehle se bana hua hai (Amazon Linux + Apache).

---

### 🔹 Step 2: Create AMI from Instance

1. Go to **EC2 Dashboard**
2. Select **Instance**
3. Click **Actions**
4. Image and templates → **Create image**
5. Enter details:

   * **Name:** `webserver-v1`
6. Configure as required
7. Click **Create Image**

---

### 🔹 Step 3: Launch Instance from AMI

1. Go to **AMIs page**
2. Select your AMI
3. Click **Launch instance**
4. Instance Name:

   * `web-server-production`
5. Select **Key pair**
6. Network settings:

   * Enable ✅ SSH
   * Enable ✅ HTTP
7. Advanced details → Paste **User Data script**:

```bash
#!/bin/bash
sudo yum update -y

# Install Apache web server
sudo yum install -y httpd

# Start Apache service
sudo systemctl start httpd

# Enable Apache on boot
sudo systemctl enable httpd

# Create a simple HTML file
echo "<html>
<h1>Welcome to Apache Web Server on Amazon Linux-$(hostname)!</h1>
</html>" > /var/www/html/index.html
```

8. Click **Launch instance**

---

### 🔹 Step 4: Verify Web Server

1. Go to **Instances**
2. Select `web-server-production`
3. Copy **IPv4 Public Address**
4. Open browser and paste IP address

✅ Apache web page successfully load ho jayega

---

## 🚀 Launch Template Creation

### 🔹 Create Launch Template from Instance

1. Go to **Instances**
2. Select instance
3. Actions → Image and templates
4. Click **Create launch template**
5. Name:

   * `my-template`
6. Configure as required
7. Click **Create Launch Template**

---

### 🔹 Launch Instance Using Launch Template

1. Go to **Launch Templates**
2. Select `my-template`
3. Launch instance
4. Go to **Instances**
5. Copy **IPv4 address**
6. Open browser

✅ Web server successfully run ho jayega

---

## 🔍 Difference: AMI vs Launch Template

| AMI                        | Launch Template          |
| -------------------------- | ------------------------ |
| OS + Software image        | Instance configuration   |
| Snapshot based             | Reusable settings        |
| Server cloning ke liye use | Automation ke liye use   |
| Instance ke liye required  | Optional but recommended |

---

## ✅ Conclusion

* **AMI** EC2 server ka blueprint hota hai
* **Launch Template** automation aur scaling ke liye useful hota hai
* **ChatGPT** scripting aur documentation ko easy banata hai

---

### 📌 Author

**Kumlesh Kurre**

---

### ⭐ Note

Kabhi bhi **.pem / .ppk files** kisi ke sath share na karein.
