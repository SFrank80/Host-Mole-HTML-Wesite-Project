# ![Alt-text](/Host an HTML Website in Default VPC.png)

---
# Host an HTML Website on a single EC2 Instance in the default VPC

This project demonstrates how to host a static HTML web application on the Amazon Web Services (AWS) cloud platform. The architecture leverages various AWS services to ensure high availability, scalability, fault tolerance, and security.

## Architecture Overview

The web application is hosted on EC2 instances within private subnets of a Virtual Private Cloud (VPC). An Application Load Balancer distributes traffic across multiple Availability Zones, routing requests to an Auto Scaling Group of EC2 instances. This setup ensures high availability and automatic scaling based on demand.

The VPC is configured with public and private subnets across two Availability Zones, enhancing fault tolerance. An Internet Gateway facilitates connectivity between the VPC instances and the Internet. Security Groups act as network firewalls, and an EC2 Instance Connect Endpoint enables secure connections to resources within both public and private subnets.

The web files are stored in a GitHub repository for version control and collaboration. A Certificate Manager secures application communications, and Simple Notification Service (SNS) alerts are configured for activities within the Auto Scaling Group. The domain name is registered and DNS records are managed using Route 53.

## User Data Script

The following user data script automates the setup and deployment of the web application on an EC2 instance:

```bash
#!/bin/bash

# Switch to the root user to gain full administrative privileges
sudo su

# Update all installed packages to their latest versions
yum update -y

# Install Apache HTTP Server
yum install -y httpd

# Change the current working directory to the Apache web root
cd /var/www/html

# Download the project GitHub repository as a ZIP file
wget https://github.com/SFrank80/Host-Mole-HTML-Wesite-Project/archive/refs/heads/main.zip

# Unzip the downloaded ZIP file
unzip main.zip

# Copy all files from the extracted repository to the Apache web root
cp -r Host-Mole-HTML-Wesite-Project-main/* /var/www/html

# Remove the extracted repository directory and the ZIP file to clean up
rm -rf Host-Mole-HTML-Wesite-Project-main main.zip

# Enable the Apache HTTP Server to start automatically at system boot
systemctl enable httpd

# Start the Apache HTTP Server to serve web content
systemctl start httpd
```

This script performs the following tasks:

1. Switches to the root user for administrative privileges.
2. Updates all installed packages to their latest versions.
3. Installs the Apache HTTP Server.
4. Changes the working directory to the Apache web root.
5. Downloads the project GitHub repository as a ZIP file.
6. Unzips the downloaded ZIP file.
7. Copies all files from the extracted repository to the Apache web root.
8. Removes the extracted repository directory and the ZIP file to clean up.
9. Enables the Apache HTTP Server to start automatically at system boot.
10. Starts the Apache HTTP Server to serve web content.

By executing this user data script on an EC2 instance, the web application will be automatically deployed and served using Apache HTTP Server.
