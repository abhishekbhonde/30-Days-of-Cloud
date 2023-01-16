# EC2

## How to create EC2 Instance?

- To launch an instance

1]  Open the Amazon EC2 console at [https://console.aws.amazon.com/ec2/v2/home](https://console.aws.amazon.com/ec2/v2/home)

2]  From the EC2 console dashboard, in the Launch instance box, choose Launch instance, and then choose Launch instance from the options that appear.

3]  Under Name and tags, for Name, enter a descriptive name for your instance.

4]  Under Application and OS Images (Amazon Machine Image), do the following:

5]  Choose Quick Start, and then choose Amazon Linux. This is the operating system (OS) for your instance.

6]  From Amazon Machine Image (AMI), select an HVM version of Amazon Linux 2. Notice that these AMIs are marked Free tier eligible. An Amazon Machine Image     (AMI) is a basic configuration that serves as a template for your instance.

7]  Under Instance type, from the Instance type list, you can select the hardware configuration for your instance. Choose the t2.micro instance type, which     is selected by default. The t2.micro instance type is eligible for the free tier. In Regions where t2.micro is unavailable, you can use a t3.micro         instance under the free tier. For more information, see AWS Free Tier.

8]  Under Key pair (login), for Key pair name, choose the key pair that you created when getting set up.

 
 
 ```
 ** Warning
Do not choose Proceed without a key pair (Not recommended). If you launch your instance without a key pair, then you can't connect to it.
  ```
  
 9]  Next to Network settings, choose Edit. For Security group name, you'll see that the wizard created and selected a security group for you. You can        use this security group, or alternatively you can select the security group that you created when getting set up using the following steps:

10]  Choose Select existing security group.

11]  From Common security groups, choose your security group from the list of existing security groups.

12]  Keep the default selections for the other configuration settings for your instance.

13]  Review a summary of your instance configuration in the Summary panel, and when you're ready, choose Launch instance.

14]  A confirmation page lets you know that your instance is launching. Choose View all instances to close the confirmation page and return to the     console.

15]  On the Instances screen, you can view the status of the launch. It takes a short time for an instance to launch. When you launch an instance, its   initial state is pending. After the instance starts, its state changes to running and it receives a public DNS name. If the Public IPv4 DNS column is hidden, choose the settings icon ( Settings icon. ) in the top-right corner, toggle on Public IPv4 DNS, and choose Confirm.

16]  It can take a few minutes for the instance to be ready for you to connect to it. Check that your instance has passed its status checks; you can view this information in the Status check column.
  
## How to create instance in video?  
  
  
[Screencast from 01-16-2023 09:53:50 PM.webm](https://user-images.githubusercontent.com/113115756/212727201-7fce4101-af93-4478-ab62-5621bc943c51.webm)
