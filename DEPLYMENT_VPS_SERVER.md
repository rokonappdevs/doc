# Deploying Incash Project on a VPS Server

## Prerequisites
- Access to a VPS (Virtual Private Server) with SSH (Secure Shell) access.
- A domain name pointing to your VPS server's IP address.

## Steps to Deploy

1. **SSH into Your VPS:**
   - Connect to your VPS using SSH. You can use a terminal or an SSH client like PuTTY.
     ```bash
     ssh username@your_server_ip
     ```

2. **Update Server Packages:**
   - Update the package repository and upgrade installed packages.
     ```bash
     sudo apt update
     sudo apt upgrade
     ```

3. **Install Required Software:**
   - Install Apache, MySQL (or MariaDB), PHP, and Git.
     ```bash
     sudo apt install apache2 mysql-server php php-mysql php-curl git openssl pdo mbstring tokenizer json gd curl zip zlib fileinfo exif
     ```

4. **Configure MySQL:**
   - Secure your MySQL installation and set a root password.
     ```bash
     sudo mysql_secure_installation
     ```

5. **Clone the Incash Project:**
   - Navigate to the appropriate directory (e.g., `/var/www`) and clone the Incash project from your Git repository.
     ```bash
     cd /var/www
     git clone -b staging https://github.com/appdevsx/incash-laravel.git
     ```

6. **Configure Apache:**
   - Create a virtual host configuration file for Incash.
     ```bash
     sudo nano /etc/apache2/sites-available/incash.conf
     ```
   - Add the following configuration (replace `your_domain` with your actual domain name):
     ```apache
     <VirtualHost *:80>
         ServerName your_domain
         DocumentRoot /var/www/incash/public

         <Directory /var/www/incash>
             AllowOverride All
         </Directory>
     </VirtualHost>
     ```
   - Enable the virtual host and restart Apache.
     ```bash
     sudo a2ensite incash
     sudo systemctl restart apache2
     ```

7. **Configure Database:**
   - Log in to MySQL as the root user and create a new database for Incash.
     ```bash
     sudo mysql -u root -p
     CREATE DATABASE incash_db;
     CREATE USER 'incash_user'@'localhost' IDENTIFIED BY 'your_password';
     GRANT ALL PRIVILEGES ON incash_db.* TO 'incash_user'@'localhost';
     FLUSH PRIVILEGES;
     EXIT;
     ```

8. **Create .env File:**
   - Create `.env` file in your project directory and copy all content from `.env.example` file. Follow the command below:
     ```bash
     cd /var/www/incash
     touch .env
     cp .env.example .env
     ```

9. **Update .env File:**
   - Navigate to the Incash project directory and update the `.env` file with your database credentials and other settings. Also update APP_URL and ASSET_URL value with your website link.
     ```bash
     cd /var/www/incash
     nano .env
     ```

10. **Install Composer Dependencies:**
   - Install Composer dependencies for the project.
     ```bash
     composer install --no-dev
     ```

11. **Run Migrations:**
    - Run database migrations to set up the database schema.
      ```bash
      php artisan migrate:fresh --seed
      ```

12. **Generate Application Key:**
    - Generate a new application key.
      ```bash
      php artisan key:generate
      ```

13. **Set File Permissions:**
    - Set appropriate permissions for the storage and cache directories.
      ```bash
      sudo chown -R www-data:www-data storage bootstrap/cache
      sudo chmod -R 775 storage bootstrap/cache
      ```

14. **Accessing the Application:**
    - Visit your domain in a web browser to access the Incash application.
      ```
      http://your_domain
      ```

15. **User Credentials:**
    - **URL:** `http://your_domain/login`
    - **Email:** user@appdevs.net
    - **Password:** appdevs

16. **Admin Login Credentials:**
    - **URL:** `http://your_domain/admin`
    - **Email:** superadmin@appdevs.net
    - **Password:** appdevs

