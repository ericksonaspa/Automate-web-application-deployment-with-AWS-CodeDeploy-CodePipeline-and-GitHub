# Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub

In this project, I will walk you through how to automate the deployment of your web application using GitHub, AWS CodeDeploy, AWS CodePipeline and EC2 instance. The following items are contained in this project.

- Create 2 IAM roles, 1 for EC2 and 1 for CodeDeploy
- Create an EC2 Instance
- 

The architecture plans to be built through this project is as follows.

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/0a12b1e6-2e46-4776-9216-3b4b3f90dbfd)

## Create 2 IAM roles, 1 for EC2 and 1 for CodeDeploy

1. We will create first an IAM role for EC2. From your AWS Management Console, search for IAM and open it in a new tab.

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/b907ff21-85e2-4d46-9046-6fab535ce1dc)

2. On the dashboard, click on **Roles** and then **Create role**. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/39542e38-66d6-4fbb-8491-009a0f53365e)

3. On the **Trusted entity type**, select **AWS service**. On the **Use case**, choose the **EC2** from the drop-down list. Then, click **Next**. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/ab7b706c-31b8-4809-8265-b043c710a3e6)

4. On the **Permission policies**, go to the search bar and search for **codedeploy**. Choose the **AmazonEC2RoleforAWSCodeDeploy** by ticking the checkbox. Scroll down and hit **Next**. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/b77abea6-5630-4944-a4d0-b60b096912d4)

5. Under the Role details, give your role a name. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/f4b8a9a1-bdd9-4a2f-b180-d68469468425)

6. Scroll down and then click **Create Role**. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/cadba7fa-d7c3-46c2-bc0e-d515b7f03bb8)

7. We will create another IAM role for CodeDeploy. Click again the **Create role** under the **IAM > Roles**. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/ad8dc29d-3f13-4223-a1ed-99b8afde7b97)

8. Scroll down then on the **Use case**, select **CodeDeploy**. Once done, click **Next**. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/506371d0-76b5-410f-bcf5-60fccae5ec2e)

9. On the **Step 2 - Add permissions**, just skip it by clicking **Next**. On the Role details, give your role a name. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/fe76709c-ea50-48f1-914e-5f4266bd33ad)

10. Scroll down, and hit **Create role**. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/69f4e0d3-c84a-48d5-a46a-8023383158e8)

11. Your 2 IAM roles should now be listed. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/c4d9b00c-4c55-44a5-976c-af978f306391)

## Create an EC2 Instance

1. From the IAM Dashboard, search for the EC2 and open it in a new tab. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/f0dd39d8-b8df-43a5-9663-e93383d57b67)

2. From your EC2 Dashboard, click the **Launch instance**. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/827f9434-b4cd-4634-a539-f2d7b0c1c62e)

3. Name your instance. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/b834491f-6b95-48e3-92e8-398c9629d3af)

4. On the **Amazon Machine Image (AMI)**, select **Amazon Linux 2 AMI (HVM)**. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/46962675-b047-4860-afdb-5bfd92cb014f)

5. For the **Instance type**, select **t2.micro**. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/8543119f-db2b-4c92-b1d7-76f430753f0b)

6. Create a key pair if you don't have one by using the hyperlink. In this screenshot, I already have one. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/78297cae-6084-406c-913b-d791c7bff26a)

7. On the **Network settings**, click **Edit** to create and modify a security group. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/c12d8587-aca9-4130-81d3-5b66222d661d)

8. Leave it with the default VPC value, and ensure that **Auto-assign public IP** is set to **Enable**. Name your security group. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/5166299b-f690-4fca-841b-289fc7fcebbe)

9. On the **Inbound rules**, add another inbound rule. Select **HTTP** on the **Type**, and choose **Anywhere** under **Source type**. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/b3b5ec6c-199b-4f42-b53d-8ba8b4c4961b)

10. Scroll down, on the **Advanced details**, look for the IAM instance profile. Select the IAM role we created earlier, **EC2CodeDeployRole**. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/86b89e13-276b-408e-81d5-77715a619b86)

11. Scroll down again, under the **User data - optional**, paste the following script:

_**#!/bin/bash
sudo yum -y update
sudo yum -y install ruby
sudo yum -y install wget
cd /home/ec2-user
wget https://aws-codedeploy-ap-south-1.s3.ap-south-1.amazonaws.com/latest/install
sudo chmod +x ./install
sudo ./install auto**_

This is the script for installing the CodeDeploy agent for Amazon Linux or RHEL. For your reference, you may refer to this link: [Install the CodeDeploy agent for Amazon Linux or RHEL](https://docs.aws.amazon.com/codedeploy/latest/userguide/codedeploy-agent-operations-install-linux.html)

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/6e046a61-b427-4bcf-8c74-ed1b7a9c53b7)

12. Once done, launch your instance. 

![image](https://github.com/ericksonaspa/Automate-web-application-deployment-with-AWS-CodeDeploy-CodePipeline-and-GitHub/assets/77118362/ecff20c8-a4c3-449c-b89c-87ddd9bcee82)

















































































