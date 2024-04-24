### Task 1. Sign into AWS Management Console

### Task 2. Launch an EC2 Instance
2.1 Click on the Services menu in the top, then click on EC2 in the Compute section, click on Launch Instance
* Name: WordPressInstance
* Choose Ubuntu
* Choose t2.micro
* Create new key wp_key 2024
* In Network Settings
   * Auto-assign public IP: Enable
   * Create new Security group: Name as MyEC2Server_SG
   * Add Inbound rule SSH Source: Custom (Allow specific IP address) or Anywhere (From ALL IP addresses accessible).
   * Add Inbound rule HTTP Source: Custom (Allow specific IP address) or Anywhere (From ALL IP addresses accessible).
   * Add Inbound rule HTTPS Source: Custom (Allow specific IP address) or Anywhere (From ALL IP addresses accessible).
* Click on Launch Instance
  ![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/7202d9e3-3df9-40be-8373-79311b53fade)


  ![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/5bce7557-f1a1-4e91-8a8e-819ff8386a9f)


### Task 3: SSH into the EC2 Instance

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/caf88d03-5d67-4916-bf3f-cede29c818a6)

### Task 4: 
4.1 To ensure that all programs are up to date, run below command:

``` 
sudo apt update -y
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/2c8622b7-1671-4b8f-afcd-e6c27afcbe95)


4.2 Install Apache server on Ubuntu

``` 
sudo apt install apache2 -y
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/793eb8cb-6567-4145-b224-55b3b80b1e8c)

4.3 Copy the public IP of instance and check if the Apache server is correctly installed or not.

```
http://54.227.204.148/
```
![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/2a047d97-2da8-47dd-b6a0-e13ed699a4cf)


4.4  Now lets install php runtime and php mysql connector
``` 
sudo apt install php libapache2-mod-php php-mysql -y
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/9e424c7a-db61-4c0b-bb7e-496fbcbd5c52)


4.4 Now we will install MySQL server for database


``` 
sudo apt install mysql-server -y
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/57933db7-89ac-45c9-956d-51b796040b68)


### TASK 5: Configuring MySQL

5.1 Install MySQL and set up a database, user and password for WordPress.

```
sudo mysql -u root
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/c67daf87-7a51-4153-825a-e7f72132d7af)

5.2 Change authentication plugin to mysql_native_password, give a strong password

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'MyPassword@123';
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/0821f642-320e-419c-88d9-4429849c6b7b)

5.3 Now lets create a new database user for wordpress, give a strong password
```
CREATE USER 'wp_user'@localhost IDENTIFIED BY 'Testpassword@123';
```
5.4 We will now create a database for wordpress

```
CREATE DATABASE wp;
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/a4d07292-b8cb-4463-b34f-cee2b4625883)

5.5 We will now grant all privilges on the database 'wp' to the newly created user

```
GRANT ALL PRIVILEGES ON wp.* TO 'wp_user'@localhost;
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/aabde510-fce5-401f-a24c-d89233591d1e)


Now Press cntl+D to come out of SQL.


### TASK 6: Now go to wordpress.org and click on Blue button Get wordpress, and you will get the new page, click on Installation Guide

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/f4bc12fa-cf87-4d5f-96ca-a0f4829e0277)

```
https://developer.wordpress.org/advanced-administration/before-install/howto-install/
```


### TASK 7. Download Wordpress now , go to cd /tmp folder

```
cd /tmp
wget https://wordpress.org/latest.tar.gz
ls
```
![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/513aedf7-2f50-487f-ac0f-787259b38be1)


Extract: Extract the WordPress files into the webserver’s document root directory (e.g., /var/www/html/).

### TASK 8. 

8.1 Unzip and unarchive installation packages to a folder called WordPress and confirm the folder.

```
tar -xzf latest.tar.gz
ls
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/1bf582b8-ad19-4ca2-bf82-4f0fa9dcaf08)


8.2 Move file into the html document route directory

```
sudo mv wordpress/ /var/www/html/
ls
cd /var/www/html
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/878de0ff-dc25-4c64-8df5-0cd7a4cac666)

### TASK 9. Now Access Installation Wizard: Open a web browser and navigate to your EC2 instance’s public IP and append wordpress or domain name to access the WordPress installation wizard.

Launch your web browser with your Public IPv4 DNS and put /wordpress as the endpoint.


```
http://54.227.204.148/wordpress
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/33f28705-8bfc-4844-ae5e-91d1d457566e)



### TASK 10: Click on Lets go and it will take you to next page

Database Setup: Enter the database details created earlier during the installation wizard.

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/8eac16b3-693d-49e2-bcfb-e6a0ea6fc065)


### TASK 11: Complete Installation: Fill in website information, create an admin account, configure the wp-config.php file with the database details and finalize the installation.

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/841c5c9a-1fb6-4b4e-9292-7d9b85b24c19)

Now copy the code which came on screen and go to the terminal, go to wordpress folder and create a new file called as wp-config.php

```
cd wordpress
vim wp-config.php
```

Copy the code which we have obatained in the error and paste in wp-config.php file and do esc: wq


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/f4e2436f-e155-444a-8e55-86950d166898)

After you’ve done that, click “Run the installation”.

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/396cde37-cd66-49e7-9ec5-cc1f73798247)


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/27a90e6b-808e-4008-8fe5-7b8daa37c21f)

Fill in all the details and Click on Submit

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/00f19590-10f9-4cf2-8839-b860dee1caea)


Click on Login, enter the Username and Password and enter and then you will be redirected to the page you have created on Wordpress.


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/6fc7a344-010f-4dbf-92ad-6d75393000bd)




