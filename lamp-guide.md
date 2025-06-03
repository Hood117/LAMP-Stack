# LAMP Stack Detailed Installation Guide on Ubuntu

## What is LAMP?

LAMP is an acronym for a popular open-source web development platform consisting of:
- **Linux** — Operating system
- **Apache** — Web server software
- **MySQL** — Relational database management system
- **PHP** — Server-side scripting language

Together, these components allow you to serve dynamic websites and web applications.

---

## Prerequisites

- Ubuntu OS (20.04, 22.04, or similar)
- User account with sudo privileges
- Internet connection

---

## Step 1: Update System Packages

```bash
sudo apt update && sudo apt upgrade -y
```
---
## Step 2: Install Apache Web Server
Apache handles HTTP requests from users and serves web pages.

```bash
sudo apt install apache2 -y
```
Check if Apache is running:

```bash
sudo systemctl status apache2
```
You can also test Apache by opening your browser and typing http://localhost or your server IP. You should see the Apache2 Ubuntu Default Page.

---
## Step 3: Adjust Firewall to Allow Web Traffic
Check available UFW application profiles:

```bash
sudo ufw app list
```

Allow Apache full profile (ports 80 and 443):

```bash
sudo ufw allow 'Apache Full'
```

Enable UFW if not already enabled:

```bash
sudo ufw enable
```
---
## Step 4: Install MySQL Database Server
```bash
sudo apt install mysql-server -y
```
Secure MySQL installation:

```bash
sudo mysql_secure_installation
```
Follow the prompts to set root password and secure your database server.

---
## Step 5: Install PHP and Modules
Install PHP along with Apache PHP module and MySQL PHP module:

```bash
sudo apt install php libapache2-mod-php php-mysql -y
```
---
## Step 6: Configure Apache to Prioritize PHP Files
Open the dir.conf file for editing:

```bash
sudo nano /etc/apache2/mods-enabled/dir.conf
```
Modify the DirectoryIndex line to prioritize index.php:

```apacheconf
<IfModule mod_dir.c>
    DirectoryIndex index.php index.html index.cgi index.pl index.xhtml
</IfModule>
```
Save and exit (Ctrl + X, then Y, then Enter).

---
## Step 7: Restart Apache to Apply Changes
```bash
sudo systemctl restart apache2
```
---
## Step 8: Test PHP Processing
Create a test PHP file:

```bash
sudo nano /var/www/html/info.php
```
Add this PHP code inside:

```php
Copy code
<?php
phpinfo();
?>
```
Save and exit.

Now open your browser and navigate to:

arduino
```http://localhost/info.php```
You should see the PHP info page with details of your PHP installation.

---
## Step 9: Test MySQL Connection with PHP
Create a PHP file to test database connection:

```bash
sudo nano /var/www/html/dbtest.php
```
Paste this code (replace username, password, and database_name with your MySQL credentials):

php
```
<?php
$conn = new mysqli("localhost", "username", "password", "database_name");

if ($conn->connect_error) {
    die("Connection failed: " . $conn->connect_error);
}
echo "Database connection successful!";
?>
```
Save and exit.

Open in browser:

arduino
```http://localhost/dbtest.php```
If successful, you’ll see “Database connection successful!”.

Important: Delete this file after testing to avoid security risks:

```bash
sudo rm /var/www/html/dbtest.php
```
Conclusion
You have successfully installed and configured the LAMP stack on Ubuntu! You can now deploy PHP-based web applications backed by MySQL databases served through Apache.
