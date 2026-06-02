## Project: Host a Website on AWS Using EC2, ALB, Route 53 and SSL
**Objective**</br>
Deploy a website on an EC2 instance and make it accessible securely through a custom domain using HTTPS.</br>
## **Architecture**
![img.png](img.png)
## Services Used
- Amazon EC2
- Application Load Balancer (ALB)
- Target Group
- Route 53
- AWS Certificate Manager (ACM)
- Security Groups
- Apache HTTP Server

## Step 1: Launch EC2 Instance
**Launch 2 or more Amazon Linux EC2 instance.**</br>
**Install Apache:**</br>
sudo yum install httpd -y</br>
**Start Apache:**</br>
sudo systemctl start httpd
sudo systemctl enable httpd
**Verify:**</br>
systemctl status httpd</br>
**Create sample page:**</br>
- echo "<h1>AWS HTTPS Project - Bijay</h1>" | sudo tee /var/www/html/index.html </br>
**Test the website:**</br>
curl localhost</br>

## Step 2: Create Target Group
**Navigate:**</br>
EC2 → Target Groups</br>
**Create:**</br>
Target Type: Instances</br>
Protocol: HTTP</br>
Port: 80</br>
Health Check Path: /index.html</br>
**Register EC2 instance.**</br>
**Verify:**</br>
Health check should be healthy</br>
**Note:-** Its checks the website reachability to consider server healthy.</br>


## Step 3: Create Application Load Balancer


