# Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database

This project demonstrates how to deploy your Python program to the EC2 instance and connect it to the RDS MySQL database. The following items are contained in this project.

- Create an IAM role
- Launch an EC2 instance, set up the security group, and execute user data
- Create an RDS database
- Connect EC2 instance to the RDS database
- Create a database table
- Clone the Python program from Git Repository
- Run the Python program
- Check program output if stored on the RDS database

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

8. Scroll down, and expand the **Additional configuration**. Put a name for your database under the **Database options > Initial database name**. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/75675fd6-5c6c-4cbd-ad8d-c946455f652d)

9. Scroll down until you reach the bottom and then click on the **Create database**. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/75c0d313-07b7-4eae-8970-b274daa6ba2b)

10. Wait for a few minutes until your database status becomes available. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/5667be8b-0506-477e-af1c-5cc68fbbb442)

### Launch your instance, connect to your database and create a table

1. Go back to the EC2 console, and click **Connect**. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/9f871296-3e05-4743-8c11-3b069e7a1197)

2. Select the **Session Manager**, and then click **Connect**. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/3427f58f-3297-4ed1-96ad-003e5a37376c)

3. Let's check if we can connect to our database. Enter the below command for us to log-in to the database.
**Format:** mysql -h {database endpoint} -P 3306 -u {master username} -p

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/6737e16b-ded7-4485-929b-ec82374dfa04)

Then, enter your master password. 

4. Once we are successfully logged-in, we will now view our databases, select our database and check its tables. See the below commands:

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/fbb83841-8245-4325-9139-2ac267769376)

5. We have verified that there are no database tables created yet for our database. We'll go ahead and create one. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/a4618052-ff50-4933-a704-9de9ad785159)

Verify if it was successfully created and then exit the sql mode. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/e369fd02-decf-4d6e-b628-65ddac8511fe)

### Clone the Python program from Git Repository

1. On your instance, run the below commands to clone the Python program from my Git Repository and change the current working folder to the repository folder. We will then be editing the python file in order to connect to our database:

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/7a13366e-ad38-43a3-8ff9-963adb79b93c)

2. Find the **ENDPOINT** inside the file and then edit its value from your **database endpoint name**. This can be found under the **Connectivity & security**. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/0f613eb7-923c-4c66-b843-27f243302dad)

3. For the **USER** and **DBNAME**, these can be found on the **Configuration** tab. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/5bd6959b-ef2e-465e-9dd1-101fe7879870)

4. Your final result should be like this below on the file: 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/48eae0f0-e7c6-4114-aafb-55d5011660df)

Ensure that you have entered also the correct password. 

5. Once done, press on your keyboard simultaneously the **Ctrl+S** to save the changes and then **Ctrl+X** to close the nano editor. 

6. Run the program by entering the commands below:

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/d5d8b953-42ed-44d5-a1f1-a4bb0e1a6af2)

### Verify if the program output is stored on the database

1. Log back in to your database. You can press the up arrow on your keyboard to view back each of the commands you run earlier. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/4f01cf35-e0e0-494b-b3e0-f7c00b8db5e1)

2. Run the below commands again to go to your databases. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/9b23ca7c-5a59-4c57-86aa-b4dcaf7d8083)

3. Enter the below command to display what is stored on your database table. 

![image](https://github.com/ericksonaspa/Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database/assets/77118362/ab13387e-e126-4165-8afc-2ab3e78fcc29)

Congratulations! As what you can see, the results after running the Python program were stored in our database. 
