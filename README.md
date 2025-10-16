# orangehrms

-------------------------------------------------------AWS Project Building-------------------------------------------------------

Building a Three Tier Application
orangehrms

OrangeHRM - Human Resource Management,
Open Source Human Resource Management Software


A LAMP stack is a bundle of four different software technologies that are used together to run applications. 

L - The operating system, Linux; 
A - The web server, Apache; 
M - The database server, MySQL; (MariaDB) 
P - The programming language, PHP. PHP (Hypertext Preprocessor) is known as a general-purpose scripting language that can be used to develop dynamic and interactive websites.
previously as Personal Home Page. It is a programming language widely used to build web applications or websites.

----Installation of Apache2 Web Server and PHP-----

Installation of Webserver and MariaDB 10.6.20
apt update

apt install apache2 -y

apt-get install software-properties-common

add-apt-repository ppa:ondrej/php

apt update

apt install php7.1

apt install php7.1 php7.1-common php7.1-mbstring php7.1-xmlrpc php7.1-soap php7.1-gd php7.1-xml php7.1-intl php7.1-mysql php7.1-cli php7.1-mcrypt php7.1-ldap php7.1-zip php7.1-curl 

-----PHP----

vi /etc/php/7.1/apache2/php.ini

file_uploads = On

allow_url_fopen = On

memory_limit = 256M

upload_max_filesize = 100M

date.timezone = America/Chicago

-------------------------------------------------------

-----AFTER INSTALATION AND ALL----

Clone the repo from the GitHub


git clone https://github.com/Shreeganesha-137/AWS-Project-Building---Three-Tier-Application.git
cd orangehrms

mv orangehrm-4.0.zip /var/www

cd /var/www

-------- if file in zip formate------

apt install unzip

unzip orangehrm-4.0.zip

mv orangehrm-4.0 orangehrm

-------------------------------------------------------

----Need to change the Apache2 permission----

chown -R www-data:www-data /var/www/orangehrm/

chmod -R 755 /var/www/orangehrm/

vi /etc/apache2/sites-available/orangehrm.conf

>>>>>> Paste this data in config file

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





a2ensite orangehrm.conf

a2enmod rewrite

systemctl restart apache2.service


-------------------------------------------------------


# AWS-Project-Building---Three-Tier-Application
