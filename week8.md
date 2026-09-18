# Week 08 Journal – Cloud Computing

**Assessment:** COIT20246 Assessment 1 Part B

**Student Name:** Rohit Hargovanbhai Prajapati  
**Student ID:** 12326317

---

# Task 1 – Knowledge Test

The Week 08 Knowledge Test was completed through Moodle as required.

The knowledge test covered fundamental concepts related to cloud computing and Microsoft Azure.

---

# Task 2 – Microsoft Learn on Demand

I successfully logged in to Microsoft Learn on Demand using the Skillable account provided for the COIT20246 tutorial.

I accessed the **COIT20246** class and entered the Microsoft Azure Fundamentals activities.

The Azure environment used for this tutorial was a temporary lab environment provided through Microsoft Learn on Demand rather than my personal Microsoft Azure account.

---

# Task 3 – Create an Azure Resource

I completed **Module 01 – Create an Azure resource** through Microsoft Learn on Demand.

The Azure resources for the activity were created in the **Australia East** region.

## Resources Created

| Resource | Purpose |
|---|---|
| Resource Group | A logical container used to organise and manage related Azure resources. |
| Storage Account | Provides cloud storage for storing data and files in Azure. |
| Virtual Network | Provides networking infrastructure that allows Azure resources to communicate. |

The resource group allows related resources to be managed together. The storage account provides cloud storage, while the virtual network provides the networking environment used by Azure resources.

**Region:** Australia East

---

# Task 4 – Create an Azure Virtual Machine and Allow Web Access

I completed **Module 02 – Create a Virtual Machine** through Microsoft Learn on Demand.

The purpose of this task was to create an Ubuntu virtual machine in Azure, install Nginx, test web access, configure a Network Security Group to allow HTTP traffic, connect to the VM using SSH, and modify the web page to include my name.

## Azure Virtual Machine Details

| Property | Value |
|---|---|
| Operating System | Ubuntu Linux |
| Region | Australia East |
| VM Purpose | Web Server |
| Web Server | Nginx |
| HTTP Port | 80 |
| SSH Port | 22 |
| Network Security | Network Security Group |
| Administrator Username | azureuser |

The Azure virtual machine provides a cloud-based Linux computer. I used the VM as a web server by installing Nginx.

---

## Creating the Virtual Machine

The virtual machine was created through the temporary Azure environment provided by Microsoft Learn on Demand.

The VM was configured with Ubuntu Linux and the required networking resources. A public IP address was assigned so that the web server could be accessed from a web browser.

### Azure CLI Commands

The following commands show the Azure CLI configuration used for the practical activity:

```bash
az group create \
  --name myResourceGroup \
  --location australiaeast
```

```bash
az vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --image Ubuntu2204 \
  --admin-username azureuser \
  --generate-ssh-keys
```

The HTTP port was then allowed for the virtual machine:

```bash
az vm open-port \
  --resource-group myResourceGroup \
  --name myVM \
  --port 80
```

---

## Installing Nginx

After creating the Ubuntu VM, I connected to the virtual machine and installed Nginx.

```bash
sudo apt update
```

```bash
sudo apt install nginx -y
```

I then checked the Nginx service:

```bash
sudo systemctl status nginx
```

Nginx is a web server that listens for HTTP requests and returns web pages to clients.

---

## Initial Website Test

Before allowing HTTP access through the Network Security Group, I attempted to access the website using the public IP address of the virtual machine.

The website returned a **connection timed out** error.

This showed that although the web server was running, incoming HTTP traffic was not yet permitted by the Azure Network Security Group.

The initial timeout was therefore useful because it demonstrated the effect of the network security configuration.

---

## Network Security Group

I opened the Network Security Group associated with the virtual machine and checked the inbound security rules.

The two relevant rules were:

| Port | Protocol | Purpose |
|---|---|---|
| 22 | TCP | Allows SSH connections for remote administration of the Ubuntu VM. |
| 80 | TCP | Allows HTTP connections to the Nginx web server. |

### Port 22 – SSH

TCP port **22** is used by Secure Shell (SSH).

SSH provides secure remote command-line access to the Ubuntu virtual machine. I used SSH to log in to the VM and modify the web page.

### Port 80 – HTTP

TCP port **80** is used by HTTP.

The HTTP rule allows a web browser to connect to the Nginx web server running on the Azure virtual machine.

---

## Adding the HTTP Security Rule

I opened:

**Azure Portal → Network Security Group → Inbound security rules → Add**

I selected **HTTP** as the service and added the rule.

The important configuration was:

```text
Service: HTTP
Port: 80
Protocol: TCP
```

After adding the rule, HTTP traffic was allowed to reach the VM.

I then accessed the website again using the VM's public IP address.

The website became accessible after the HTTP rule was added.

---

## SSH Connection

I connected to the Ubuntu virtual machine using SSH.

The SSH command used was:

```bash
ssh -l azureuser IPADDRESS
```

where `IPADDRESS` represents the public IP address assigned to the Azure virtual machine.

If a host key verification error occurs, the following command can be used:

```bash
ssh -l azureuser IPADDRESS -o StrictHostKeyChecking=no
```

After successfully connecting, I was able to access the Ubuntu command line remotely.

---

## Editing the Web Page

After connecting through SSH, I edited the default Nginx web page using:

```bash
sudo nano /var/www/html/index.html
```

I modified the HTML page to display my name.

The page content was:

```html
<!DOCTYPE html>
<html>
<head>
    <title>COIT20246 Azure Web Server</title>
</head>
<body>
    <h1>Rohit Hargovanbhai Prajapati</h1>
    <p>COIT20246 Cloud Computing</p>
    <p>Azure Virtual Machine running Nginx</p>
</body>
</html>
```

I saved the file and exited the Nano editor.

---

## Final Website Test

After modifying the HTML file, I refreshed the website in the browser.

The Nginx web server displayed the updated web page containing my name:

**Rohit Hargovanbhai Prajapati**

This confirmed that:

- The Azure virtual machine was running.
- Ubuntu was operating correctly.
- Nginx was installed and serving the web page.
- HTTP port 80 was allowed through the Network Security Group.
- SSH provided remote access to the VM.
- The web page could be modified from the Ubuntu VM.
- The updated web page could be accessed through the VM's public IP address.

### Final Website Evidence

**Screenshot required:** A screenshot of the web browser successfully accessing the website with the page displaying **Rohit Hargovanbhai Prajapati**.

> **Insert actual Azure browser screenshot here before submission.**

```text
[FINAL WEBSITE SCREENSHOT]
```

---

## Public IP Address

The VM was assigned a public IP address for external access.

**Public IP Address:** `[Insert the actual public IP address from the Azure lab]`

The public IP address should be copied from the Azure Portal because the Microsoft Learn on Demand environment uses temporary Azure resources.

---

# Task 5 – Compare Cloud vs On-Premise Costs

The purpose of this task was to compare a consumer desktop PC with a similar cloud virtual machine.

The comparison considers the specifications, upfront cost, one-year cost, and three-year cost.

For the cloud VM, the Azure Pricing Calculator is used. For the consumer desktop PC, an Australian online computer retailer is used.

## Computer Comparison

| Specification | Consumer Desktop PC | Azure Virtual Machine |
|---|---|---|
| Deployment | Physical/on-premise | Cloud |
| Location | User premises | Azure Australia East |
| CPU | Comparable consumer CPU | Comparable Azure VM CPU |
| RAM | Comparable RAM | Comparable RAM |
| Storage | Local storage | Cloud/managed storage |
| Upfront Hardware Cost | Required | No physical server purchase |
| Running Cost | Electricity and maintenance | Azure usage charges |
| Scalability | Requires hardware upgrade | VM size can be changed |
| Maintenance | User/organisation responsibility | Physical infrastructure managed by Azure |

The exact desktop specification and Azure calculator price depend on the options selected during the tutorial. The specifications should satisfy the limits provided by the tutor.

---

## Upfront Cost

A consumer desktop PC normally requires the hardware to be purchased before it can be used. The upfront cost includes the computer hardware.

An Azure virtual machine does not require the user to purchase the physical server. Instead, the user pays for cloud resources according to the selected configuration and usage.

---

## One-Year and Three-Year Costs

The cost comparison should consider:

- Initial hardware purchase cost.
- Azure VM running cost.
- Electricity costs for the physical computer.
- Possible maintenance and upgrade costs.
- Storage and other cloud resource charges where applicable.

| Period | Consumer Desktop PC | Azure VM |
|---|---:|---:|
| Upfront | Hardware purchase | No physical hardware purchase |
| 1 Year | Hardware + operating costs | Azure usage costs |
| 3 Years | Hardware + operating costs | Azure usage costs |

The Azure Pricing Calculator should be used to obtain the actual Azure estimate required for the assessment.

---

## Trade-offs

### Advantages of a Consumer Desktop PC

- The physical hardware is owned by the user.
- It can be used locally without depending on an Internet connection for many workloads.
- There are no ongoing cloud VM usage charges after purchasing the hardware.
- Hardware may be upgraded when required.

### Disadvantages of a Consumer Desktop PC

- A relatively large upfront purchase may be required.
- The owner is responsible for maintenance and repairs.
- The available computing capacity is limited by the hardware.
- Electricity is required during operation.
- Scaling generally requires purchasing or upgrading physical hardware.

### Advantages of an Azure Virtual Machine

- Physical server hardware does not need to be purchased.
- A VM can be created relatively quickly.
- Computing resources can be selected according to requirements.
- VM resources can be scaled or changed when requirements change.
- The underlying cloud infrastructure is managed by Microsoft Azure.

### Disadvantages of an Azure Virtual Machine

- Costs can continue while chargeable resources are running.
- Internet access is normally required for remote access.
- Long-term costs depend on the VM configuration and usage.
- Poor resource management can result in unnecessary cloud costs.
- Cloud services introduce dependency on the service provider.

---

# Task 6 – Create a Storage Blob

Task 6 was listed as an **optional** activity in the Week 08 tutorial.

The activity involved creating an Azure Storage Blob, uploading multiple images, and configuring different access levels.

The activity demonstrates how Azure Storage can be used to store files and how access controls can determine whether objects are private or publicly readable.

---

# Task 7 – Create a Resource Lock

Task 7 was listed as an **optional** activity in the Week 08 tutorial.

A resource lock can help protect Azure resources from accidental modification or deletion.

## Read-only Lock

A read-only lock prevents changes to a protected resource while allowing the resource to be viewed.

## Delete Lock

A delete lock prevents the protected resource from being deleted while still allowing permitted changes to the resource.

Resource locks can therefore provide an additional protection mechanism for important Azure resources.

---

# Reflection

This week's activities provided practical experience with Microsoft Azure and cloud computing.

Creating an Azure virtual machine helped me understand how a computer system can be provided as a cloud resource instead of requiring physical hardware. I also gained practical experience with Ubuntu Linux and Nginx.

The Network Security Group activity demonstrated the importance of controlling network traffic. SSH uses TCP port 22 for remote administration, while HTTP uses TCP port 80 for web traffic. Adding the HTTP rule allowed the browser to communicate with the Nginx web server.

Using SSH to modify `/var/www/html/index.html` also helped me understand how a Linux-based cloud server can be managed remotely. After modifying the page, I could access the updated website through the VM's public IP address.

The cloud versus on-premise comparison helped me understand that the two approaches have different cost models. A physical computer normally requires an upfront hardware investment, while a cloud VM uses an ongoing resource-based pricing model.

Overall, the Week 08 activities improved my understanding of Azure virtual machines, Network Security Groups, SSH, HTTP, Nginx, cloud storage, resource protection, and the financial trade-offs between cloud and on-premise computing.

---
