# Local Server Deployment Instructions for Incash Project

## Prerequisites
- Download and install XAMPP local server for Windows with PHP 8.1 from [this link](https://sourceforge.net/projects/xampp/files/XAMPP%20Windows/8.1.25/xampp-windows-x64-8.1.25-0-VS16-installer.exe/download).
- Download and install Composer on your local machine from [this link](https://getcomposer.org/Composer-Setup.exe).
- Ensure that the following PHP extensions are enabled: gd, curl.

## Steps to Deploy
1. **Start XAMPP Server:**
   - Launch XAMPP and start both Apache and MySQL services.

2. **Database Setup:**
   - Access the MySQL database dashboard by navigating to [localhost/phpmyadmin](http://localhost/phpmyadmin) in your web browser.
   - Create a new database for the Incash project.

3. **Project Setup:**
   - Download and unzip the Incash project files.
   - Open the project in your preferred IDE.

4. **Configuration:**
   - Open the `.env` file located in the project root directory.
   - Update the following fields with your database credentials:
     ```
     DB_DATABASE=your_database_name
     DB_USERNAME=your_database_username
     DB_PASSWORD=your_database_password
     ```

5. **Terminal Commands:**
   - Open the terminal in your IDE and navigate to the project root directory.
   - Run the following commands:
     ```
     composer update
     composer dumpautoload
     php artisan migrate:fresh --seed
     php artisan key:generate
     php artisan serve
     ```

6. **Accessing the Application:**
   - Open your web browser and visit one of the following URLs:
     - [http://127.0.0.1:8000](http://127.0.0.1:8000)
     - [http://localhost:8000](http://localhost:8000)
   - You should see the index page of the Incash project.

## User Credentials

- **URL:** [http://127.0.0.1:8000/login](http://127.0.0.1:8000/login)
- **Email:** user@appdevs.net
- **Password:** appdevs

## Admin Login Credentials

- **URL:** [http://127.0.0.1:8000/admin](http://127.0.0.1:8000/admin)
- **Email:** superadmin@appdevs.net
- **Password:** appdevs
