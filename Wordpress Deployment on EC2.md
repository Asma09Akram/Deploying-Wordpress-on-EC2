### Task 1. Sign into AWS Management COnsole
### Task 2. Launch an EC2 Instance
2.1 Click on the Services menu in the top, then click on EC2 in the Compute section, click on Launch Instance
* Name: WordPressInstance
* Choose Amazon Linux 2023 AMI
* Choose t2.micro
* Create new key wp_key
* In Network Settings
   * Auto-assign public IP: Enable
   * Create new Security group: Name as MyEC2Server_SG
   * Add Inbound rule SSH Source: Custom (Allow specific IP address) or Anywhere (From ALL IP addresses accessible).
   * Add Inbound rule HTTP Source: Custom (Allow specific IP address) or Anywhere (From ALL IP addresses accessible).
   * Add Inbound rule HTTPS Source: Custom (Allow specific IP address) or Anywhere (From ALL IP addresses accessible).
* Click on Launch Instance

  ![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/5bce7557-f1a1-4e91-8a8e-819ff8386a9f)


Task 3: SSH into the EC2 Instance
I have used Putty to SSH into newly created EC2 Instance

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/04aa05c8-9456-40c9-821e-fff1339b679d)

Task 4: 
4.1 To ensure that all programs are up to date, run below command:
``` sudo yum update -y ```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/e80ddd27-6d17-4fab-8042-fe451e2df676)

4.2  Install Apache: Use ‘dnf’ package managers to install Apache webserver because the latest one in 2023) can only be installed by ‘dnf’ 
``` sudo dnf install php -y ```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/fc50e665-bae9-4c28-805f-0e53dce86c67)


4.3  Install MySQL or MariaDB and set up a database, user and password for WordPress.
``` sudo yum install httpd ```



4.4 Install PHP and necessary PHP modules required by WordPress.

``` sudo dnf install -y wget php-fpm php-mysqli php-json php php-devel   ```


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/682e9d85-becc-4397-8132-788b56627866)



![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/18a7e809-e3a1-42fc-85b7-be22f0143d8e)



STEP 3: Configuring MySQL/MariaDB

Install MySQL or MariaDB and set up a database, user and password for WordPress. We would be installing MariaDB server.
```
sudo dnf install mariadb105-server
dnf info mariadb105
```
![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/df7ef65b-f2bd-440f-a5a6-7fde8348d62c)


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/fceccdac-5185-402b-81b0-009cf94a713d)

```dnf info mariadb105```


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/91784474-c25f-4aae-ac60-cbe7973ad9be)


```
sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo systemctl status mariadb
```



![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/aaaafd93-76e8-45f9-9888-a80cf433cd82)

LOG ON AND CREATE A NEW PASSWORD FOR MYSQL

Secure the MySQL installation
```
sudo mysql_secure_installation

```


Ensure to change the password to your preferred password.
Type Y to remove the anonymous user accounts.
Type Y to disable the remote root login.
Type Y to remove the test database.
Type Y to reload the privilege tables and save your changes.


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/72267164-723d-4cd8-ab9b-5c2cec6943fd)

Login with your new password to access the database

```sudo mysql -u root -p
```

Create a new database and a dedicated user for WordPress and grant appropriate privileges to the user on the WordPress database.

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/aa008147-f4a4-4097-a82f-01365a8fd08c)


Create a new database and a dedicated user for WordPress and grant appropriate privileges to the user on the WordPress database.


```
CREATE USER 'wordpress-user'@'localhost' IDENTIFIED BY 'your_strong_password';

CREATE DATABASE `wordpress-db`;

CREATE DATABASE `wordpress-db`;

FLUSH PRIVILEGES;

exit

```




![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/3b9a48ef-49be-4a5e-be0b-e363b7d3150a)













































4.3.1 Install MySQL or MariaDB and set up a database, user and password for WordPress. We would be installing MariaDB server.

``` sudo dnf install mariadb105-server
dnf info mariadb105
```


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/7a92f236-24bc-4bf5-bedf-4b33414c9d46)

``` sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo systemctl status mariadb ```


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/a098bc8e-e8e1-4056-a897-7b5dd9f75577)


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/25e746db-7a90-45b9-81da-6792e136717d)


4.4 Start the Apache Server
``` sudo systemctl start httpd ```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/29cdbae6-eb18-40cd-bd4d-c795bf8251e6)

4.5 We can also make the apache server start automatically every time we boot the instance with following command:

``` sudo systemctl enable httpd ```


4.6 Test whether Apache Server enabled or not with below command:
``` sudo systemctl is-enabled httpd ```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/e94dcb1e-c25e-4698-9f78-dc721a9ca1cd)


4.7 Install PHP and necessary PHP modules required by WordPress.

```sudo dnf install -y wget php-fpm php-mysqli php-json php php-devel``` 

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/f5be933c-72f8-4a0f-b032-ae1115aec319)

4.7 Copy the Public IPv4 address and enter in your browser and hit enter. If you see the below test page, it means apache server is successfully installed.



### Task 5: Setting up permissions and LAMP server

5.1 Add user (ec2-user) to apache group
``` sudo usermod -a -G apache ec2-user ```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/addd7849-3412-4ec3-a920-9261e3a3dc5b)


5.2 Log out and log back in to verify the membership of the new group

Execute the logout command or close the window:
``exit```

SSH into the instance again

To verify membership enter the below command:
```groups```


5.3 Change the group ownership of /var/www and the content inside of it to the apache group:

```sudo chown -R ec2-user:apache /var/www ```

5.4 Now add group write permissions, to set the group ID on future subdirectories and also change the directory permissions of /var/www and its subdirectories:
``` sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/bf5ae006-be6d-4c26-97c1-d85bd72ed34f)

5.5 To add group write permissions, recursively change the file permissions of /var/www and its subdirectories:

```find /var/www -type f -exec sudo chmod 0664 {} \;```


5.6 Now, the EC2 user (and any future members of the apache group) can add, delete, and edit files in the root of the Apache document. This allows you to add content like a static website or a PHP application.



Let's test the LAMP server now.

We will create a PHP file at the root of the Apache document. This will become our home page to test if everything is working as expected.

``` echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
```

5.6 To test the example PHP page, open a tab in the browser and enter "/phpinfo.php" after the Public IPv4 address as shown in the below image.

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/fecbf825-74b9-455a-a01e-1a92a7d80a9d)


5.7 Now that we have tested the example site, we can delete the phpinfo.php file.

5.8 Let's delete the phpinfo.php file. We just used it to test, for security reasons, these details should not be available on the internet.

```rm /var/www/html/phpinfo.php
```



### Task 6: Database Server Security Details


To start the MariaDB server:

```sudo systemctl start mariadb```
To install MySQL, run the mysql_secure_installation.

```sudo mysql_secure_installation```
When prompted for a password, type a password for the root account. (by default, the root account does not have a password). Press Enter when finished.

Type Y to set the password, and retype the password to confirm it.

Note: Make a note of the new password which you set as it will be used in future. Password@1234

Type Y  to remove the anonymous user accounts.

Type Y  to disable the remote root login.

Type Y  to remove the test database.

Type Y to reload the privilege tables and save your changes.

Optional: We can also make the MariaDB server start on every boot, . If you would like to enable this, type the following command:


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/633a9aef-1716-4ca2-96f5-4aec20b4b56c)

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/b99a72dc-2dd5-44a4-b199-313334e6e713)

```sudo systemctl enable mariadb```


Task 7: Optional installation for handling the administration of MySQL over the Web with phpMyAdmin
Let's install the required dependencies:

```sudo yum install php-mbstring php-xml -y```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/0c88b4fb-a11b-4a7a-912c-f7650809789c)

Restart the Apache Server:

```sudo systemctl restart httpd```
We also need to restart php-fpm.

```sudo systemctl restart php-fpm```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/de7d7e91-d82c-4843-a548-9e0a00762b2c)

Navigate to the root of the Apache document at /var/www/html.

```cd /var/www/html```
We have to select a source package for the latest phpMyAdmin release from https://www.phpmyadmin.net/downloads. To download the file directly to your instance, copy the link and paste it into a wget command as shown below:

```wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.tar.gz```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/c585bc30-75e1-45fa-9dfa-d5e6b86207f4)

Create a phpMyAdmin folder and extract the package into it with the following command:

```mkdir phpMyAdmin && tar -xvzf phpMyAdmin-latest-all-languages.tar.gz -C phpMyAdmin --strip-components 1```



Delete the phpMyAdmin-latest-all-languages.tar.gz tarball.

```rm phpMyAdmin-latest-all-languages.tar.gz```


Run the following command to make sure MySQL is running:

```sudo systemctl start mariadb```
In a web browser, type the below URL to see the php admin page:

http://yourIPAddress/phpMyAdmin

http://http://13.200.222.110/phpMyAdmin

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/723a6626-b647-4883-83e8-0c8fe47db19c)

Log into your phpMyAdmin installation with your root user name and the MySQL root password we created earlier.

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/9dae5ba9-93c1-41a0-8753-e3708874d1b9)


