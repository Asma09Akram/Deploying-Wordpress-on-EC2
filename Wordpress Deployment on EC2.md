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
``` sudo yum update -y
```

![image](https://github.com/Asma09Akram/Deploying-Wordpress-on-EC2/assets/124654068/e80ddd27-6d17-4fab-8042-fe451e2df676)

4.2 
