# Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database

This project demonstrates how to deploy your Python program to the EC2 instance and connect it to the RDS MySQL database. 

### Create an IAM role

1. On the AWS Management Console, search for the IAM console and open it in a new tab. In the navigation pane, choose **Roles**, and then choose **Create role**.

![image](https://github.com/ericksonaspa/Highly-Available-and-Scalable-Web-Application/assets/77118362/4f65edb4-5e95-46db-b4a8-dcde291c3069)

![image](https://github.com/ericksonaspa/Highly-Available-and-Scalable-Web-Application/assets/77118362/2b825fb9-0d02-4f94-8de4-3b8cb788bac2)

2. Under **Select type of trusted entity**, choose **AWS service**. Immediately under **Choose the service that will use this role**, choose **EC2**, and then choose **Next**.

![image](https://github.com/ericksonaspa/Highly-Available-and-Scalable-Web-Application/assets/77118362/6626e733-2e79-42f1-b54e-e291aac5f97f)

3. On the **Attach permissions** policies page, do the following: Use the **Search** field to locate the **AmazonSSMManagedInstanceCore**. Select the box next to its name. Choose **Next**.

![image](https://github.com/ericksonaspa/Highly-Available-and-Scalable-Web-Application/assets/77118362/86a70df9-3d71-4c53-9ba9-dca737e0438e)

4. For Role name, enter a name for your new instance profile, such as **SSMInstanceProfile**. Choose **Create role**. The system returns you to the **Roles** page. 

![image](https://github.com/ericksonaspa/Highly-Available-and-Scalable-Web-Application/assets/77118362/897bd207-1a10-4bd7-9cde-69f0a0239ff0)

### Launch an instance

1. From your AWS Management Console, search for the **EC2** and open it in a new tab.

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/65ed5118-dad8-42ef-83e2-945913a0c5fc)

2. On the EC2 Dashboard, go to the **Instances** under **Instances** and then click the **Launch instances**. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/dcd8f152-8764-44d1-8415-2c6345253255)

3. On the next page, name your instance. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/aff73b81-961f-4540-b1d6-7aa5e997d0fd)

Ensure that the following defaults are selected: 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/75e46533-9ad7-45ab-ab01-c06145c121f9)

4. For the **Instance type**, select the **t2.micro**. Then **Proceed without a key pair (Not recommended)** since we won't be using SSH and will Session Manager instead. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/aa907b95-bdeb-4c1d-8e4b-f7bb08dc9173)

5. Click **Edit** on the **Network Settings**, select **Create security group**. Name your Security group and its description. Ensure that the Auto-assign public IP is set to **Enable**. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/08ebb0c2-6f65-434b-9801-1d22698fa492)

6. On the **Inbound Security Group Rules**, allow TCP/80 traffic by adding the **HTTP** on the **Type** and **My IP** on the Source type. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/b400105a-e4a5-4ec6-8250-0b76d86b0e40)

7. Expand the Advanced details, then on the IAM instance profile, select the IAM role we created earlier. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/c3a371ec-e09a-4a2b-a24f-af64fbe7b57e)

8. Scroll down, and enter the below commands on the **User data**. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/5dbc8313-d07f-44ba-a48a-044ee3eec339)

9. Review the Summary and then click on the **Launch instance**. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/186a33be-ae10-4270-86bb-809f55dd5ec1)

### Create an RDS instance

1. From your dashboard, search for **RDS** and open it in a new tab. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/ec586101-e5e2-4b3d-af20-9dc4274dbe20)

2. On your RDS dashboard, click on the **Create database**. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/f41b2d0d-dc52-4239-8c60-5aea763b91fb)

3. On the **Choose a database creation method**, select the **Standard create**. Then **MySQL** on the **Engine options**. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/7928e613-6b59-4295-a3e6-087acece8a69)

4. On the Templates, select the **Free Tier**. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/af8dbc46-d612-4ad9-a5ab-d47db92121a5)

5. Put a name for your **DB instance identifier**, create a username and password. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/635deb1d-fb70-439d-8fc6-bfcf6aa58692)

6. On the **Connectivity**, choose the **Connect to an EC2 compute resource**. Under the **EC2 instance**, select the EC2 instance we created earlier. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/f62dc866-35d9-4aa1-b1be-df07a2ef34ec)

7. On the **VPC security group (firewall)**, choose **Create new** then name your security group. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/e85ebfeb-3447-48be-ba42-52f1a392cc2b)

8. Scroll down, expand the **Additional configuration**. Put a name for your database under the **Database options > Initial database name**. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/39cef3a6-4446-4691-a2db-ddbd8dbf880a)

9. Scroll down until you reach the bottom and then click on the **Create database**. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/75c0d313-07b7-4eae-8970-b274daa6ba2b)

10. Wait for a few minutes until your database status becomes available. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/5667be8b-0506-477e-af1c-5cc68fbbb442)










































































































