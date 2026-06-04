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
- Create a webpage and put it inside /var/www/html/index.html </br>
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
**Navigate:**</br>
EC2 → Load Balancers</br>
**Create:**</br>
Type: Application Load Balancer</br>
Scheme: Internet-facing</br>
**Listeners**</br>
HTTP : 80</br>
**Availability Zones:**</br>
Select at least 2 Ability Zone</br>
**Attach:**</br>
Target Group</br>

## Step 4: Configure Security Groups
**ALB Security Group**</br>
Inbound:</br>
80   0.0.0.0/0
443  0.0.0.0/0

**EC2 Security Group**</br>
Inbound:</br>
80  Source = ALB Security Group</br>
22  Your IP</br>

## Step 5: Create Route 53 Hosted Zone
**Navigate:**
Route 53 → Hosted Zones</br>
**Create**</br>
lerntechnology.online</br>
Copy Name Servers</br>
Update Name Servers at domain registrar.</br>

## Step 6: Request SSL Certificate
**Navigate:**</br>
AWS Certificate Manager</br>
**Request:**</br>
lerntechnology.online</br>
www.lerntechnology.online</br>
**Validation:**</br>
DNS Validation</br>
Create validation records in Route 53.</br>
**Wait until:**
Issued</br>
## Step 7: Add HTTPS Listener
**Navigate:**</br>
ALB → Listeners</br>
**Add:**</br>
Protocol: HTTPS</br>
Port: 443</br>
**Select:**
ACM Certificate</br>
lerntechnology.online
**Forward to:**</br>
Target Group</br>
