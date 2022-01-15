# COMP6573001-2021-Clyde
A 5th semester Cloud project, intended to advance our skills in understanding Cloud and Distributed System.

Teammates:
1. Jeconiah Richard [2301947905]
Github: github.com/niaguraa

## Steps

**1. Create S3 Bucket**

In my case, I named it "clyde-project-bucket". This bucket is to store the website files needed to run it on cloud. Your HTML, CSS, along side with the other files correlating with the website should be stored here.

**2. Create VPC**

Leave settings as default

**3. Create Internet Gateway**

Create the Public Subnets. In my case, I create 2 Public Subnets with different regions. Then enable the "Enable auto-assign public IPv4 address" in Subnet settings.

**4. Create Route Tables**

Create a new Route Table, then connect the previous subnets to it. Assign the public subnets to public route table.
*note: What differs public subnet to private is that Public Subnet has Internet Gateway attached to the Route Table*


**5. Create IAM Roles**
- SSM Role = To test run EC2 to the Internet (AmazonSSMFullAccess)
- S3 Role = To download S3 bucket contents to EC2 Instance (AmazonS3FullAccess)

**6. Create Security Group for Application Load Balancer**
a. Auto Load Balancer (ALB) Security Group
- Inbound rules: HTTP and HTTPS from 0.0.0.0/0 (anywhere)

b. SSH Security Group
- Inbound rules: SSH with "My IP" as source

c. Web Security Group
- In bound rules: HTTP and HTTPS (ALB Security Group as Source) and SSH (SSH Security Group as source)


**7. Create EC2**
- First, Create key pair
- Create instances
In this case, I made 2 Instances for 2 Private Subnets. In Step 6 of making the Instance, select WebServer Security Group for both instances
- Use the existing key pair we made to launch the instance


**8. Create Load Balancer**
In the creation of Load Balancer, select your VPC and select your Public Subnets for the Availability Zone.
- Select ALB Security Group
- Create Target Group
- Route your "index.html" file in S3 to perform health check
