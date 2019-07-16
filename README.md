# Qwinix-assignment
The deployment was successful, however after adding required parameter input the template is not working. I am still working on it.

Features Completed
Created Virtual Network(Vnet)
Created 3 Subnet
-	1 for Bastion
-	1 for Webservers 
-	1 DB server
Created Scale set on for both Bastion and Webserver with Ubuntu VMs, and General purpose DDsv1  
-	For Bastion Scale set parameter was to set Min 1VM and Max 1 VM at autoscaling 
-	For Webserver scale set parameter set as Min2 VM and Max 10 vm wrt to CPU threshold 80 increase by 1 vm and if CPU below 20% VM downscale by 1 VM
Cloud init Script used – 
#!/bin/bash
yum update -y
yum install httpd -y
service httpd start
chkconfig httpd on
cd /var/www/html
echo "<html><h1>IaC challenge completed: Akash Sharma</h1></html>"  >  index.html 
 
Created Load balancer for both Bastion and Webserver
-	For bastion Load balancer Type – Public, SKU – Basic, Public IP- Assigned new static public IP on Frontend IP configuration, Backend Pool created for Bastion Scale set, Default Health probe,
Bastion load balancer is created just to make the Public IP static for VM scale set VM instance
-	For Webserver Loadbalancer – Type Public, SKU – Basic, Public ip assigned, Backend pool – Webserver, 

Network security group for Bastion – Allow all SSH traffic 
Network Security group for Web server – Allow all HTTP traffic from anywhere, Allow SSH from Bastion SUBNET range only.

Deployed instance for postraceSQL server – standard and single machine was taken as to connect it with PrivateDB subnet.
We created public blob with read access and enabled managed identies for Webserver scale set and added it as blob contributor.

Monitoring- Created alert for creation and deletion on VMs in Wwebserver scale set


