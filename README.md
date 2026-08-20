# AWS-LOAD-BALANCER
### REG NUMBER: 212224040270
### NAME: RANJANA R
## AIM
To use Elastic Load Balancing (ELB) and Auto Scaling services to load balance and automatically scale an AWS infrastructure.

## ALGORITHM
### Step 1: Create an AMI for Auto Scaling
Open the EC2 console, confirm that Web Server 1 is running (2/2 status checks passed), select the instance, and choose Actions → Image and templates → Create image. Name it "WebServerAMI" and create it. This AMI will be used to launch identical instances later.

### Step 2: Create a Target Group and Load Balancer
Create a Target Group named "LabGroup" (type: Instances, VPC: Lab VPC) without registering targets yet. Then create an Application Load Balancer named "LabELB" under Lab VPC, mapped to Public Subnet 1 and Public Subnet 2, using the Web Security Group, with the HTTP:80 listener forwarding to LabGroup.

### Step 3: Create a Launch Template and Auto Scaling Group
Create a Launch Template named "LabConfig" using the WebServerAMI, instance type t2.micro, key pair "vockey", the Web Security Group, and Detailed CloudWatch monitoring enabled. Using this template, create an Auto Scaling group named "Lab Auto Scaling Group" attached to Private Subnet 1 and Private Subnet 2, linked to the LabGroup target group, with desired/minimum/maximum capacity of 2/2/6 and a target tracking scaling policy set to maintain 60% average CPU utilization.

### Step 4: Verify Load Balancing
Confirm that two new "Lab Instance" EC2 instances were launched by Auto Scaling and that both show a "healthy" status in the LabGroup target group. Copy the Load Balancer's DNS name and open it in a browser to confirm the application is being served correctly through the load balancer.

### Step 5: Test Auto Scaling
Lower the scaling policy's target CPU value to 50% to make scaling trigger sooner, then use the application's "Load Test" feature to generate high CPU load across the instances. Monitor the CloudWatch alarms (AlarmLow/AlarmHigh) until AlarmHigh enters the "In alarm" state, then verify in the EC2 console that additional instances were automatically launched to handle the load.

### Step 6: Terminate the Original Web Server
Select Web Server 1 (the original instance used to create the AMI) and terminate it, since it is no longer needed once the Auto Scaling group is managing instances independently.

## OUTPUT

<img width="1919" height="1145" alt="Screenshot 2026-08-18 091540" src="https://github.com/user-attachments/assets/8d37d997-e3cf-4ebd-bd56-4429fd8b4d40" />

<img width="1919" height="1149" alt="Screenshot 2026-08-18 091708" src="https://github.com/user-attachments/assets/78067273-03d3-4850-9e78-cc08044ee77e" />

<img width="1918" height="1143" alt="Screenshot 2026-08-18 091902" src="https://github.com/user-attachments/assets/04750cf0-94ce-4c42-b183-a35dab7c873b" />

<img width="1919" height="1150" alt="Screenshot 2026-08-18 091942" src="https://github.com/user-attachments/assets/39906d72-c0b2-4761-adcc-71a473de3552" />

<img width="1919" height="1136" alt="Screenshot 2026-08-18 092243" src="https://github.com/user-attachments/assets/a95f6c19-1b0e-4826-bd9b-71b19aff681a" />

<img width="1919" height="1148" alt="Screenshot 2026-08-18 092302" src="https://github.com/user-attachments/assets/865fa04d-e26e-46be-acad-f96de1fd99ea" />

<img width="1919" height="1146" alt="Screenshot 2026-08-18 092442" src="https://github.com/user-attachments/assets/114b22f0-568e-42c3-823a-3182bd9c5b55" />

<img width="1919" height="1153" alt="Screenshot 2026-08-18 092712" src="https://github.com/user-attachments/assets/f50f4b58-fe58-4c68-8e03-cf7d753617cd" />

<img width="1919" height="1141" alt="Screenshot 2026-08-18 092728" src="https://github.com/user-attachments/assets/e3b46943-e6ca-4b88-8eed-9fde7f7d2443" />

<img width="1919" height="1143" alt="Screenshot 2026-08-18 093306" src="https://github.com/user-attachments/assets/42e72a47-c407-43df-b460-0e0b2d0dd936" />

<img width="1919" height="1146" alt="Screenshot 2026-08-18 093331" src="https://github.com/user-attachments/assets/c706634e-ae98-42ba-b5fa-995247169b0f" />

<img width="741" height="1600" alt="WhatsApp Image 2026-08-20 at 11 05 53 AM" src="https://github.com/user-attachments/assets/96cc338e-e51d-4558-aee4-33c56bfce952" />

<img width="743" height="1600" alt="WhatsApp Image 2026-08-20 at 11 05 53 AM (1)" src="https://github.com/user-attachments/assets/403e43ac-f709-441d-84f7-e255e4e37c6d" />

<img width="1916" height="1142" alt="Screenshot 2026-08-20 110827" src="https://github.com/user-attachments/assets/374fe0b4-f305-440b-85e3-8b05d3f3e108" />

<img width="1918" height="1039" alt="Screenshot 2026-08-20 110736" src="https://github.com/user-attachments/assets/9b0cd2b9-b9db-4260-8b0f-35666a7958fd" />

<img width="1919" height="1087" alt="Screenshot 2026-08-20 111015" src="https://github.com/user-attachments/assets/697e990f-2708-4393-87a4-44affe66490a" />

<img width="1919" height="1109" alt="Screenshot 2026-08-20 111024" src="https://github.com/user-attachments/assets/4da6c628-4a70-476b-96de-a5c7472d4272" />

## RESULT
Thus, an AMI was created from a running EC2 instance, a Load Balancer was configured to distribute traffic across multiple instances, an Auto Scaling group was set up with a target tracking scaling policy, and the infrastructure was verified to automatically scale out under increased load using CloudWatch alarms.
