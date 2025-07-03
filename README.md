
# MarketPeak_Ecommerce Deployment Documentation

This README describes the complete process used to deploy the **MarketPeak_Ecommerce** website on an AWS EC2 instance, along with branch management and web content creation using Git.

---

##  Project Overview

MarketPeak_Ecommerce is a simple HTML-based project (based on the Tooplate template) deployed to a live web server using Apache on Amazon EC2. Git is used for version control and collaboration.

---

##  Prerequisites

Before starting, ensure the following are available:

- An [AWS EC2](https://aws.amazon.com/ec2/) instance running Amazon Linux 2
- SSH key (`.pem` file) to connect to the EC2 instance
- GitHub repository (e.g., [https://github.com/Attehfirst/MarketPeak_Ecommerce](https://github.com/Attehfirst/MarketPeak_Ecommerce))
- Apache web server installed
- Git installed

---

##  Step-by-Step Deployment Process

###  1. Initialize Git Repository

```bash
mkdir MarketPeak_Ecommerce
cd MarketPeak_Ecommerce
git init
```
![alt text](image-1.png)

### 1.2 Using a Template from Tooplate

###  Download and Extract

```bash
wget https://www.tooplate.com/zip-templates/2130_waso_strategy.zip
unzip 2130_waso_strategy.zip
```

### 1.3 Stage and commit the template to Git

```
git add .
git config --global user.name "YourUsername"
git config --global user.email "youremail@example.com"
git commit -m "Initial commit with basic e-commerce site structure"

```

### 1.4 Push the code to your github repository

```
git remote add origin https://github.com/your-git-username/MarketPeak_Ecommerce.git
git push -u origin main

```

### 2. AWS Deployment

To deploy "MarketPeak_Ecommerce" platform, you’ll start by setting up an Amazon EC2 instance:

### 2.1. Set Up an AWS EC2 Instance

Log in to the AWS Management Console.

Launch an EC2 instance using an Amazon Linux AMI.

Connect to EC2 Instance via SSH

```bash
ssh -i "Ecomm.pem" ec2-user@34.235.87.105
```

### 2.2 Clone the repository on the Linux server

![alt text](image-2.png)

> Generate SSH keys with `ssh-keygen`, and add the `.pub` key to GitHub → Settings → SSH Keys.

---

![alt text](image.png)

- Display and publish your publlic key

```
[ec2-user@ip-172-31-26-190 ~]$ cat /home/ec2-user/.ssh/id_rsa.pub

```

![alt text](image-3.png)

- Add SSH Public key to Github Account

```bash
git clone git@github.com:Attehfirst/MarketPeak_Ecommerce.git

```

###  2.3 Install Required Packages

```bash
# Install Apache
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd

# Install Git
sudo yum install git -y

# (Optional) Install wget/unzip if downloading templates

``
sudo yum install wget unzip -y
```

### 2.4 Configure httpd for website

```
sudo rm -rf /var/www/html/*
sudo cp -r ~/MarketPeak_Ecommerce/* /var/www/html/

```

- Reload httpd: Apply the changes by reloading the httpd service.

```
sudo systemctl reload httpd
```

###  2.5. Access Website from Browser

With httpd configured and website files in place, MarketPeak Ecommerce platform is now live on the internet:

Open a web browser and access the public IP of your EC2 instance to view the deployed website.

![alt text](image-4.png)



###  3. Continuos integration and deployment workflow

- Step 1
  Developing a new feature - Adding an html file.

  ```
  git branch development
  git checkout development

```

- Step 2
  Version control unit

```
git add .
git commit -m "Add new features or fix bugs"
git push origin development


- Step 3
Pull request and merging to the main branch

```
git checkout main
git merge development
git push origin main

```

- Step 4
 Deploying updates to the Production server

 ```
 git pull origin main
 sudo systemctl reload httpd

```

Step 5 
Testing the new changes



## 📌 Tips & Troubleshooting

- Ensure EC2 Security Group has **port 80 (HTTP)** open to the public
- If site shows **"It works!"**, you likely haven't replaced Apache's default index.html
- Always check you're in a Git repository (`ls -a` should show `.git`)



##  Useful Commands Reference

```bash
# Start Apache
sudo systemctl start httpd

# Check Apache status
sudo systemctl status httpd

# List branches
git branch

# Switch branch
git checkout branch-name

# See Git status
git status
```

---

## ✅ Summary

With these steps, you have:
- Set up Apache on EC2
- Deployed a website using Git and a Tooplate template
- Managed branches and added new pages
- Committed and pushed changes to GitHub

---

## 👨‍💻 Author

Fred Atteh  
GitHub: [@Attehfirst](https://github.com/Attehfirst)

---
