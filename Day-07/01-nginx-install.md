Understanding Your Setup
You've correctly laid the foundation for securing your web application:

Resource Group: A container for related Azure resources.
Virtual Network (VNet): A private network within Azure.
Linux VM: A virtual machine running Linux.
Nginx Server: A web server installed on the VM.
Web Page: Your content hosted on the Nginx server.
Implementing Selective IP Access
To restrict access to your web page to specific IP addresses, you'll primarily use Network Security Groups (NSGs). Here's a breakdown of the steps:

1. Create a Network Security Group (NSG)
Navigate to your resource group in the Azure portal.
Click on "Network security groups" and create a new NSG.
Assign a name to the NSG.
2. Configure Inbound Security Rules
In the NSG, go to "Inbound security rules".
Create new rules with the following settings:
Priority: A unique number for each rule (lower numbers take precedence).
Source: Specify the allowed IP addresses or IP ranges (e.g., your public IP, a specific range).
Source port ranges: Any (or specific ports if needed).
Destination port ranges: 80 (for HTTP) or 443 (for HTTPS).
Protocol: TCP.
Action: Allow.
Create a rule to deny all other traffic:
Priority: Higher than the allow rules.
Source: Any.
Source port ranges: Any.
Destination port ranges: Any.
Protocol: Any.
Action: Deny.
3. Associate NSG with the Virtual Network Subnet
Go to your virtual network.
Select the subnet where your VM resides.
In the "Network security group" section, associate the created NSG with the subnet.
Additional Security Considerations
While using NSGs is a good starting point, consider implementing these additional measures for enhanced security:

1. Azure Firewall
For more complex firewalling needs, explore Azure Firewall. It offers advanced features like application-level filtering, intrusion prevention, and URL filtering.
2. Public IP Address Configuration
Consider using a static public IP address for your VM instead of a dynamic one. This provides a consistent endpoint for allowed IP addresses.
3. SSH Access Restrictions
Limit SSH access to your VM using public key authentication and restrict access to specific IP addresses.
4. Application-Level Security
Implement web application firewalls (WAFs) to protect against common web attacks.
Use strong passwords and encryption for your web application.
5. Monitoring and Logging
Enable Azure Monitor to track network traffic, security alerts, and VM performance.
Testing Your Configuration
Access your web page from allowed IP addresses to verify functionality.
Attempt to access the web page from blocked IP addresses to ensure it's inaccessible
# Install and Configure Nginx on Ubuntu

## Step 1: Update Package Lists

Before installing any new software, it's a good practice to update the package lists to ensure you get the latest version.

```bash
sudo apt update
sudo apt upgrade
```

## Step 2: Install Nginx

Install Nginx using the following command:

```
sudo apt install nginx
```

## Step 3: Start Nginx Service

```
sudo systemctl start nginx
```

## Step 4: Create HTML File

```
sudo vim /var/www/html/index.html
```

Add the HTML content, for example.

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Demo Page</title>
</head>
<body>
    <h1> I Learnt how networking works in Azure today</h1>
</body>
</html>
```

Save the file.

### Restart Nginx

```
sudo systemctl restart nginx
```









