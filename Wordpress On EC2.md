Install WordPress

Connect to your instance, and download the WordPress installation package

Download and install these packages using the following command.

```
sudo dnf install wget php-mysqlnd httpd php-fpm php-mysqli mariadb105-server php-json php php-devel -y

```


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/4cd03c19-f22b-4432-bb70-feb1c998ef29)



![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/f61deeae-eb41-47c0-8013-ce6f463f7b38)


2. Download the latest WordPress installation package with the wget command. The following command should always download the latest release.

```

wget https://wordpress.org/latest.tar.gz
```


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/4973efe8-d46f-4f06-b379-11a364f42923)


3. Unzip and unarchive the installation package. The installation folder is unzipped to a folder called wordpress.

```
tar -xzf latest.tar.gz
  ```


To create a database user and database for your WordPress installation
Your WordPress installation needs to store information, such as blog posts and user comments, in a database. This procedure helps you create your blog's database and a user that is authorized to read and save information to it.

Start the database and web server.

```
sudo systemctl start mariadb httpd

```
Log in to the database server as the root user. Enter your database root password when prompted; this may be different than your root system password, or it might even be empty if you have not secured your database server.

If you have not secured your database server yet, it is important that you do so.

Run mysql_secure_installation.

```
sudo mysql_secure_installation
```

When prompted, type a password for the root account.

Type the current root password. By default, the root account does not have a password set. Press Enter.

Type Y to set a password, and type a secure password twice. For more information about creating a secure password, see https://identitysafe.norton.com/password-generator/. Make sure to store this password in a safe place.

Setting a root password for MariaDB is only the most basic measure for securing your database. When you build or install a database-driven application, you typically create a database service user for that application and avoid using the root account for anything but database administration.

Type Y to remove the anonymous user accounts.

Type Y to disable the remote root login.

Type Y to remove the test database.

Type Y to reload the privilege tables and save your changes.


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/7ca053f8-9272-487a-b63d-f34e8bf665c9)


Step 4: (Optional) Install phpMyAdmin

phpMyAdmin is a web-based database management tool that you can use to view and edit the MySQL databases on your EC2 instance. 
Follow the steps below to install and configure phpMyAdmin on your Amazon Linux instance.

```
mysql -u root -p
```
Password@1234

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/ccda15ea-45a7-42f7-aefd-8a2aa1fdd133)


* Create a user and password for your MySQL database. Your WordPress installation uses these values to communicate with your MySQL database. Enter the following command, substituting a unique user name and password.

```
CREATE USER 'wordpress-asma'@'localhost' IDENTIFIED BY 'Password@2024';

```
Make sure that you create a strong password for your user. Do not use the single quote character ( ' ) in your password, because this will break the preceding command. Do not reuse an existing password, and make sure to store this password in a safe place.

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/6d6022c7-09f9-49e9-82e4-e4e24cd2bc67)



* Create your database. Give your database a descriptive, meaningful name, such as wordpress-db.

```
CREATE DATABASE `wordpress-db`;
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/21582c95-167b-4fa8-9a21-3340fe06e056)


* Grant full privileges for your database to the WordPress user that you created earlier.

```
GRANT ALL PRIVILEGES ON `wordpress-db`.* TO "wordpress-asma"@"localhost";
  ```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/24367896-b0df-46e8-a0d9-c9ff8af9f2cd)


* Flush the database privileges to pick up all of your changes.

  ```
  FLUSH PRIVILEGES;
  ```
  
  
![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/2149543d-7e5e-4524-a861-0414e7544c69)


* Exit the mysql client.

  ```
  exit
  ```

To create and edit the wp-config.php file
The WordPress installation folder contains a sample configuration file called wp-config-sample.php. In this procedure, you copy this file and edit it to fit your specific configuration.

Copy the wp-config-sample.php file to a file called wp-config.php. This creates a new configuration file and keeps the original sample file intact as a backup.

```
cp wordpress/wp-config-sample.php wordpress/wp-config.php
```
* Edit the wp-config.php file with your favorite text editor (such as nano or vim) and enter values for your installation. If you do not have a favorite text editor, nano is suitable for beginners.

  ```
  vim wordpress/wp-config.php

  ```

  ![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/748be0db-b3e3-49c3-8d47-26f81d9ad744)


Find the line that defines DB_NAME and change database_name_here to the database name that you created in Step 4 of To create a database user and database for your WordPress installation.
Find the line that defines DB_USER and change username_here to the database user that you created earlier
Find the line that defines DB_PASSWORD and change password_here to the strong password that you created earlier

```
define('DB_NAME', 'wordpress-db');
define('DB_USER', 'wordpress-asma');
define('DB_PASSWORD', 'your_strong_password');
```

To install your WordPress files under the Apache document root

Now that you've unzipped the installation folder, created a MySQL database and user, and customized the WordPress configuration file, you are ready to copy your installation files to your web server document root so you can run the installation script that completes your installation. The location of these files depends on whether you want your WordPress blog to be available at the actual root of your web server (for example, my.public.dns.amazonaws.com) or in a subdirectory or folder under the root (for example, my.public.dns.amazonaws.com/blog).

If you want WordPress to run at your document root, copy the contents of the wordpress installation directory (but not the directory itself) as follows:

```
sudo cp -r wordpress/* /var/www/html/
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/856d9f72-d8c7-4aae-b2f4-aff6bfbcb267)


If you want WordPress to run in an alternative directory under the document root, first create that directory, and then copy the files to it. In this example, WordPress will run from the directory blog:

```
sudo mkdir /var/www/html/blog
sudo cp -r wordpress/* /var/www/html/blog/

```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/44f35fb7-2d1a-47bc-a930-fac503e85f49)


To allow WordPress to use permalinks
WordPress permalinks need to use Apache .htaccess files to work properly, but this is not enabled by default on Amazon Linux. Use this procedure to allow all overrides in the Apache document root.

Open the httpd.conf file with your favorite text editor (such as nano or vim). If you do not have a favorite text editor, nano is suitable for beginners.


```
sudo vim /etc/httpd/conf/httpd.conf
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/abe6f45a-14fa-4efa-8e4b-d7b267de4e8c)


Find the section that starts with <Directory "/var/www/html">.


Change the AllowOverride None line in the above section to read AllowOverride All.


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/950a54f2-ddac-4534-b7a7-1733c1eb7696)



Save the file and exit your text editor.


