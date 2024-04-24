### Task 1. Sign into AWS Management COnsole

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


STEP 3: Configuring MySQL

3.1 Install MySQL and set up a database, user and password for WordPress.

```
sudo mysql -u root
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/c67daf87-7a51-4153-825a-e7f72132d7af)

3.2 Change authentication plugin to mysql_native_password, give a strong password

```
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'MyPassword@123';
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/0821f642-320e-419c-88d9-4429849c6b7b)

3.3 Now lets create a new database user for wordpress, give a strong password
```
CREATE USER 'wp_user'@localhost IDENTIFIED BY 'Testpassword@123';
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










