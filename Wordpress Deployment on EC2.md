![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/3d45ea81-429f-4faf-a1dd-eb12eac73a7b)### Task 1. Sign into AWS Management COnsole
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


Task 3: SSH into the EC2 Instance

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/caf88d03-5d67-4916-bf3f-cede29c818a6)

Task 4: 
4.1 To ensure that all programs are up to date, run below command:

``` 
sudo yum update -y
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/2c8622b7-1671-4b8f-afcd-e6c27afcbe95)


4.2 Install Apache server on Ubuntu
sudo apt install apache2

``` 
sudo apt install apache2 -y
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/793eb8cb-6567-4145-b224-55b3b80b1e8c)

4.3 Copy the public IP of instance and check if the Apache server is correctly installed or not.
```
http://54.227.204.148/
```
![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/2a047d97-2da8-47dd-b6a0-e13ed699a4cf)


4.4  Now lets install Install php runtime and php mysql connector
``` 
sudo apt install php libapache2-mod-php php-mysql -y
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/9e424c7a-db61-4c0b-bb7e-496fbcbd5c52)


4.4 Install PHP and necessary PHP modules required by WordPress.

``` 
sudo dnf install -y wget php-fpm php-mysqli php-json php php-devel
```


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

```
sudo mysql -u root -p
```

Create a new database and a dedicated user for WordPress and grant appropriate privileges to the user on the WordPress database.

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/aa008147-f4a4-4097-a82f-01365a8fd08c)


Create a new database and a dedicated user for WordPress and grant appropriate privileges to the user on the WordPress database.


```
CREATE USER 'wordpress-asma'@'localhost' IDENTIFIED BY 'your_strong_password';

CREATE DATABASE `wordpress-db`;

CREATE DATABASE `wordpress-db`;

FLUSH PRIVILEGES;

exit

```




![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/3b9a48ef-49be-4a5e-be0b-e363b7d3150a)



STEP 4: Downloading and Configuring WordPress:

Navigate to the /tmp directory and fetch the latest WordPress package from the official WordPress website.

```
cd /tmp
wget https://wordpress.org/latest.tar.gz
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/8e25fc11-a5dd-47f9-855d-e03cb6c4a32d)


Extract: Extract the WordPress files into the webserver’s document root directory (e.g., /var/www/html/).

Unzip and unarchive installation packages to a folder called WordPress and confirm the folder.

```
tar -xzf latest.tar.gz
```



Move file into the html document route directory

```
sudo mv wordpress/ /var/www/html/
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/c61f8723-4df6-45c3-a0fa-17499381fe54)


STEP 5: WordPress Installation:

Access Installation Wizard: Open a web browser and navigate to your EC2 instance’s public IP or domain name to access the WordPress installation wizard.

Launch your web browser with your Public IPv4 DNS and put /wordpress as the endpoint.


```
ec2-3-110-32-180.ap-south-1.compute.amazonaws.com/wordpress/
```


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/32e97a82-3128-472f-9f08-b83479a5d926)


STEP 6: Database Setup: Enter the database details created earlier during the installation wizard.
STEP 7: Complete Installation: Fill in website information, create an admin account, configure the wp-config.php file with the database details and finalize the installation.


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/200f0b7a-3505-43ad-a5fe-7af97197b3ab)


To create and edit the wp-config.php file
The WordPress installation folder contains a sample configuration file called wp-config-sample.php. In this procedure, you copy this file and edit it to fit your specific configuration.


Copy the wp-config-sample.php file to a file called wp-config.php. This creates a new configuration file and keeps the original sample file intact as a backup.


![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/522cccb1-2179-4e88-870d-167499515f93)










