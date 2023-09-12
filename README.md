# Deploy-Python-program-to-the-EC2-instance-and-connect-it-to-RDS-MySQL-database

This project demonstrates how to deploy your Python program to the EC2 instance and connect it to the RDS MySQL database. 

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








































































































































