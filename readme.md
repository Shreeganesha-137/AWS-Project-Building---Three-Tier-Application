>>>>>>>>>>>>>>>>>>.....>🟠 OrangeHRM Three-Tier AWS Project<<<<<<<<<<<<<<<<<<<<<<<
>>>>>>>>>>>>>>>>>>>
🚀 Deploying OrangeHRM on AWS using LAMP Stack (Linux, Apache, MySQL, PHP)

📘 Project Overview

This project demonstrates how to deploy the open-source OrangeHRM (Human Resource Management System) using a three-tier architecture on AWS Cloud.
It utilizes a LAMP stack — Linux, Apache, MySQL (MariaDB), and PHP — to host the application on an EC2 instance, connected to a secure database backend.

This setup follows best practices for scalability, security, and modularity — making it ideal for DevOps and cloud beginners.

🧱 Architecture Diagram

Three-Tier Architecture:

Client (Browser)
       |
       v
  Web Tier (Apache + PHP on EC2)
       |
       v
  App Tier (OrangeHRM Codebase)
       |
       v
  DB Tier (MariaDB/MySQL on RDS or EC2)

🧩 AWS Services Used

Service	Purpose
EC2	Host the web server and OrangeHRM application,
RDS / EC2 (Private)	Host MariaDB/MySQL database,
VPC	Network isolation with public and private subnets,
Security Groups	Control inbound and outbound traffic,
IAM	Manage permissions and access,
S3 (optional)	Store backups or static assets,

⚙️ Tech Stack
Layer	Technology
OS	Ubuntu 22.04 LTS
Web Server	Apache2

Backend Language	PHP 7.1
Database	MariaDB 10.6

Application	OrangeHRM (Open Source)
🔧 Installation Steps

1️⃣ Launch EC2 Instance

Ubuntu 22.04 LTS

Security Group: Allow HTTP (80) and SSH (22)

2️⃣ Install Apache and PHP

sudo apt update -y

sudo apt install apache2 -y

sudo apt-get install software-properties-common -y

sudo add-apt-repository ppa:ondrej/php -y

sudo apt update -y

sudo apt install php7.1 php7.1-common php7.1-mbstring php7.1-xmlrpc php7.1-soap php7.1-gd php7.1-xml php7.1-intl php7.1-mysql php7.1-cli php7.1-zip php7.1-curl -y

3️⃣ Install MariaDB and Create Database

sudo apt install mariadb-server -y

sudo mysql_secure_installation

sudo mysql -u root -p

CREATE DATABASE orangehrm CHARACTER SET utf8;

CREATE USER 'orangeuser'@'%' IDENTIFIED BY 'orange123';

GRANT ALL PRIVILEGES ON orangehrm.* TO 'orangeuser'@'%';

FLUSH PRIVILEGES;

EXIT;

4️⃣ Clone OrangeHRM Repository
cd /tmp
git clone https://github.com/SHRIDHARMUDASHI/orangehrms.git
cd orangehrms
sudo mv orangehrm-4.0.zip /var/www
cd /var/www
sudo apt install unzip -y
sudo unzip orangehrm-4.0.zip
sudo mv orangehrm-4.0 orangehrm

5️⃣ Set Permissions and Configure Apache
sudo chown -R www-data:www-data /var/www/orangehrm/
sudo chmod -R 755 /var/www/orangehrm/


Create Virtual Host:

sudo vi /etc/apache2/sites-available/orangehrm.conf


Paste:

<VirtualHost *:80>
    ServerAdmin admin@example.com
    DocumentRoot /var/www/orangehrm
    ServerName example.com
    ServerAlias www.example.com

    <Directory /var/www/orangehrm/>
        Options +FollowSymlinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>


Enable the site:

sudo a2ensite orangehrm.conf
sudo a2enmod rewrite
sudo systemctl restart apache2
