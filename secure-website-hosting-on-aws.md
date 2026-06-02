## Project: Host a Website on AWS Using EC2, ALB, Route 53 and SSL
**Objective**</br>
Deploy a website on an EC2 instance and make it accessible securely through a custom domain using HTTPS.</br>
**Architecture**
Internet
│
▼
https://lerntechnology.online
│
▼
Route 53
│
▼
Application Load Balancer
(HTTPS : 443)
│
▼
Target Group
│
▼
EC2 Instance
Apache (80)