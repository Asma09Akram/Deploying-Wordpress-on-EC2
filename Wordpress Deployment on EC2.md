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

4.2 Now get the latest versions of MariaDB (a community-developed fork of MySQL) and PHP. Run the following commands to install them both:
``` sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2 ```


4.3 Now lets install Apache server and MariaDB.
``` sudo yum install -y httpd mariadb-server ```


4.4 Start the Apache Server
``` sudo systemctl start httpd ```


4.5 We can also make the apache server start automatically every time we boot the instance with following command:

``` sudo systemctl enable httpd ```


4.6 Test whether Apache Server enabled or not with below command:
``` sudo systemctl is-enabled httpd ```


4.7 Copy the Public IPv4 address and enter in your browser and hit enter. If you see the below test page, it means apache server is successfully installed.



### Task 5: Setting up permissions and LAMP server

5.1 Add user (ec2-user) to apache group
``` sudo usermod -a -G apache ec2-user ```

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


5.5 To add group write permissions, recursively change the file permissions of /var/www and its subdirectories:

```find /var/www -type f -exec sudo chmod 0664 {} \;```


5.6 Now, the EC2 user (and any future members of the apache group) can add, delete, and edit files in the root of the Apache document. This allows you to add content like a static website or a PHP application.



Let's test the LAMP server now.

We will create a PHP file at the root of the Apache document. This will become our home page to test if everything is working as expected.

``` echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php
```

5.6 To test the example PHP page, open a tab in the browser and enter "/phpinfo.php" after the Public IPv4 address as shown in the below image.


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

Note: Make a note of the new password which you set as it will be used in future.

Type Y  to remove the anonymous user accounts.

Type Y  to disable the remote root login.

Type Y  to remove the test database.

Type Y to reload the privilege tables and save your changes.

Optional: We can also make the MariaDB server start on every boot, . If you would like to enable this, type the following command:

```sudo systemctl enable mariadb```


Task 7: Optional installation for handling the administration of MySQL over the Web with phpMyAdmin
Let's install the required dependencies:

```sudo yum install php-mbstring php-xml -y```

Restart the Apache Server:

```sudo systemctl restart httpd```
We also need to restart php-fpm.

```sudo systemctl restart php-fpm```
Navigate to the root of the Apache document at /var/www/html.

```cd /var/www/html```
We have to select a source package for the latest phpMyAdmin release from https://www.phpmyadmin.net/downloads. To download the file directly to your instance, copy the link and paste it into a wget command as shown below:

```wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.tar.gz```
Create a phpMyAdmin folder and extract the package into it with the following command:

```mkdir phpMyAdmin && tar -xvzf phpMyAdmin-latest-all-languages.tar.gz -C phpMyAdmin --strip-components 1```


Delete the phpMyAdmin-latest-all-languages.tar.gz tarball.

```rm phpMyAdmin-latest-all-languages.tar.gz```


Run the following command to make sure MySQL is running:

```sudo systemctl start mariadb```
In a web browser, type the below URL to see the php admin page:

http://yourIPAddress/phpMyAdmin

Log into your phpMyAdmin installation with your root user name and the MySQL root password we created earlier.


