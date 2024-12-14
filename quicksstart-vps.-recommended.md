---
icon: user-beard-bolt
description: >-
  This guide is for installion on a digital ocean droplet, linode or ec2
  machine. The installation guide assumes your are using Ubuntu 24.04 and LAMP
---

# Quicksstart VPS. (Recommended)



***

**Step-by-Step Installation Instructions for Memex on a VPS**

**Prerequisites:**

1. **LAMP Stack**: Make sure you have a LAMP (Linux, Apache, MySQL, PHP) server setup. This setup includes: ([Server Requirements for full list](https://app.gitbook.com/o/YKDZy1exkkindRHOQGS7/s/m8taPuNBtN7T73vrTCU5/prerequisites))
   * **Linux** (Ubuntu or CentOS, for instance)
   * **Apache** web server
   * **MySQL 8.0** database server (or MariaDB, depending on your preference)
   * **PHP 8.2 or later** (preferably the latest version compatible with Memex)
2. **Composer** and **Node.js/NPM** installed on your server:
   * **Composer**: A dependency manager for PHP, required to install PHP packages.
   * **Node.js and NPM**: Node Package Manager, required for frontend assets.\\

**Detailed Steps: We shall be deploying to a domain&#x20;**_<mark style="color:red;">**"memex.io"**</mark>_

1. **Set Up Your Web Root**:
   * Point your Apache web server’s DocumentRoot to the `public` directory inside your site directory.
   * Example for Apache configuration for memex.io site. replace memex.io with your own domain.
   *   (`/etc/apache2/sites-available/memex.io.conf`):

       ```apacheconf
       <VirtualHost *:80>
           ServerName memex.io
           DocumentRoot /var/www/memex.io/public
           
           <Directory /var/www/memex.io/public>
               AllowOverride All
               Require all granted
           </Directory>

           ErrorLog ${APACHE_LOG_DIR}/memex.io-error.log
           CustomLog ${APACHE_LOG_DIR}/memex.io-access.log combined
       </VirtualHost>
       ```
2.  After updating this file, enable the site and restart Apache:

    <pre class="language-bash"><code class="lang-bash"><strong>sudo a2ensite memex.io.conf
    </strong>sudo systemctl reload apache2
    </code></pre>
3. **Clone The repo. to you site folder**
   1. <pre class="language-bash"><code class="lang-bash">cd /var/www/
      <strong>git clone https://github.com/scriptoshi/memex.git  memex.io
      </strong><strong>// In apache config above DocumentRoot is /var/www/memex.io
      </strong></code></pre>
4. **If you cannot clone above, simply download from github and extract the Application Files**:
   * Dowload memex files  and Upload the zip your to your `/var/www/` directory.
   *   Extract the zip file:

       ```bash
       sudo unzip Memex-vps.zip -d /var/www/
       ```
   *   Rename the extracted folder to your site name, for example:

       ```bash
       sudo mv /var/www/Memex /var/www/memex.io
       ```
5. **Navigate to the Site Directory**:
   *   Change directory to your newly created site folder:

       ```bash
       cd /var/www/memex.io
       ```
6. **Install PHP Dependencies**:
   *   Run Composer to install the necessary PHP packages:

       ```bash
       composer install
       ```
   * This will create a `vendor` directory containing all the required PHP packages.
7. **Set Up Frontend Assets**:
   *   Run NPM to build frontend assets:

       ```bash
       npm install
       npm run production
       ```
8. **Configure Environment Variables**:
   *   rename the `env.example` file to `.env`:

       ```bash
       cp .env.example .env
       ```
   *   Update `.env` with your database and other configuration details:

       ```basic
       DB_CONNECTION=mysql
       DB_HOST=127.0.0.1
       DB_PORT=3306
       DB_DATABASE=your_database_name
       DB_USERNAME=your_database_user
       DB_PASSWORD=your_database_password

       #APIKEYS
       #usdrates api (free apikey https://coincap.io/api-key)
       COINCAP_APIKEY="55014acc-....-c042809054da"
       #appkit project id: https://cloud.reown.com/
       PROJECT_ID="0908f6dccf.....a07b199620c"
       ## Ankr apikey https://www.ankr.com/rpc/projects/
       ANKR_KEY="601613d5ca8940e....0690e421efc9d81"

       #ADMIN-ACCESS
       ADMIN="0xcf01271DC73639843e95C24F7FA3C0b11A1a9B27"
       ```
9. **Generate Application Key**:
   *   Run the following command to generate a unique application key:

       <pre class="language-bash"><code class="lang-bash"><strong>php artisan key:generate
       </strong></code></pre>
10. **Run Database Migrations and Seeders**:
    *   Migrate the database tables and seed initial data:

        ```bash
        php artisan migrate --seed
        ```
11. **Set Folder Permissions**:
    *   Ensure the necessary permissions for the `storage` and `bootstrap/cache` directories:

        ```bash
        sudo chmod -R 775 storage bootstrap/cache
        sudo chown -R www-data:www-data storage bootstrap/cache
        ```
12. **Restart Apache**:
    *   Finally, restart Apache to ensure all configurations are correctly applied:

        ```bash
        sudo systemctl restart apache2
        ```
13. **Access the Site**:
    * Open your browser and navigate to your site’s URL (e.g., `http://memex.io`). Your site should now be live!
14. **Clean up and fix a few things.**
    *   If you are like me , you most likely use root, so some permission maybe messed up. \\

        ```bash
        # Clean up
        mkdir -p storage/app/public/uploads/
        php artisan clear-compiled
        php artisan optimize
        php artisan storage:link
        sudo chgrp -R www-data storage bootstrap/cache
        sudo chmod -R ug+rwx storage bootstrap/cache
        ```

Open your browser and navigate to your site’s URL (e.g., `http://memex.io`). Your site should now be live!



### Configure CRON

**Option 1: Using Crontab**

1. Open your crontab file:

```bash
crontab -u www-data -e
```

2. Add this line to run the scheduler every minute:

```bash
* * * * * cd /path-to-your-project && php artisan schedule:run >> /dev/null 2>&1
```

Replace `/path-to-your-project` with your  project path. _**(Not the public directory)**_

**Option 2: Using System Crontab**

1. Create a new file in `/etc/cron.d/`:

```bash
sudo nano /etc/cron.d/laravel-scheduler
```

2. Add the following line:

```bash
* * * * * www-data cd /path-to-your-project && php artisan schedule:run >> /dev/null 2>&1
```

3. Set proper permissions:

```bash
sudo chmod 644 /etc/cron.d/laravel-scheduler
```

### SETUP LARAVEL REVERB.

You need to setup supervisor to run reverb:start. We include a bash script to get you up and running. make sure you are in your site directory. This will rig and start all the supervisor processes needed to get reverb up and running. correctly

```bash
#cd to your site directory EG.cd /var/www/memex.com
cd /var/www/memex.io
chmod +x laravel-reverb-setup.sh
sudo bash ./laravel-reverb-setup.sh
```

***

Update `.env`

```bash
#update REVERB_HOST with your plain domain.
#Donot add a slash after or http(s). eg scriptoshi.com, memex.website.com etc
REVERB_HOST="scriptoshi.com"

```



### Laravel Queue Workers.

The app users queues for events for Jobs, Events and Notification.  Queue workers are monitored by supervisord. We have created  bash script that will configure supervisord to monitor your queues. here's how to run it.

```bash
#cd to your site directory EG.cd /var/www/memex.io
cd /var/www/memex.io
chmod +x queue-worker-setup.sh
sudo bash./queue-worker-setup.sh
```
