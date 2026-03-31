# Create Virtual Cloud Networks

## Introduction

Oracle Cloud Infrastructure (OCI) Compute lets you create multiple Virtual Cloud Networks (VCNs). These VCNs will contain security lists, compute instances, load balancers and many other types of network assets.

Be sure to review [Overview of Networking](https://docs.cloud.oracle.com/iaas/Content/Network/Concepts/overview.htm) to gain a full understanding of the network components and their relationships, or take a look at this video:

[](youtube:mIYSgeX5FkM)

Estimated Time: 15 minutes

Here is an instructional video, going through the process of making a VCN:

[](youtube:eOGPej8n_ws)

### Objectives
In this lab, you will:
- Explore how to create a virtual cloud network
- Explore Public and Private Subnets
- Explore the different gateways: Internet, NAT, Service
- Explore Route Tables 
- Explore Security Lists & Network Security Groups

### Prerequisites

* An Oracle Cloud Account - please view this workshop's LiveLabs landing page to see which environments are supported.

>**Note:** If you have a **Free Trial** account, when your Free Trial expires, your account will be converted to an **Always Free** account. You will not be able to conduct Free Tier workshops unless the Always Free environment is available. 

**[Click here for the Free Tier FAQ page.](https://www.oracle.com/cloud/free/faq.html)**

## Task 1: Create Your VCN using the Wizard

<if type="livelabs">
You are running this workshop in a LiveLabs environment. Our LiveLabs environments use a pre-configured Virtual Cloud Network (VCN), so you will not create a VCN in this workshop. However, you can see how a VCN is created in Oracle Cloud Infrastructure by watching this short video:

 [](youtube:lxQYHuvipx8)
 </if>

<if type="freetier">
To create a VCN on Oracle Cloud Infrastructure:

1. On the Oracle Cloud Infrastructure Console Home page, under the **Launch Resources** header, click **Set up a network with a wizard**.

    ![Setup a Network with a Wizard](images/setup-vcn.png " ")

2. Click the **Actions** dropdown and select **Start VCN Wizard**.

    ![Setup a Network with a Wizard](images/actions-dropdown.png " ")

3. Select **Create VCN with Internet Connectivity**, and then click **Start VCN Wizard**.

    ![Start VCN Wizard](images/start-wizard.png " ")

4. Complete the following fields:

    |                  **Field**              |    **Value**  |
    |----------------------------------------|:------------:|
    |VCN Name |OCI\_HOL\_VCN|
    |Compartment |  Choose the ***Demo*** compartment you created in the ***Identity and Access Management Lab***
    |VCN CIDR Block|10.0.0.0/16|
    |Public Subnet CIDR Block|10.0.0.0/24|
    |Private Subnet CIDR Block|10.0.1.0/24|
    |Use DNS Hostnames In This VCN| Checked|

    Your screen should look similar to the following:

    ![Create a VCN Configuration|Foobar](images/vcn-configuration.png " ")

     Click the **Next** button at the bottom of the screen.

5. Review your settings to be sure they are correct. Click the **Create** button to create the VCN. 
    ![Review CV Configuration](images/review-vcn.png " ")

6. It will take a moment to create the VCN and a progress screen will keep you apprised of the workflow.

    ![Workflow](images/workflow.png " ")

7. Once you see that the creation is complete (see previous screenshot), click the **View Virtual Cloud Network** button.
</if>

## Task 2: Public and Private Subnets
Within a VCN, you have subnets. Subnets are subdivisions of a VCN. Each subnet in a VCN consists of one or more contiguous range of IPv4 addresses and optionally IPv6 addresses that don't overlap with other subnets in the VCN. Subnets act as a unit of configuration comprised of: a route table, security lists, and DHCP options. Subnets can either be public or private. We will go over each type in this task.

### Public Subnets
When you create a subnet, by default it's considered public, which means instances in that subnet are allowed to have public IPv4 addresses and internet communication is permitted with IPv6 endpoints. In order to connect to the internet, you must use an Internet Gateway which will enable inbound and outbound internet connectivity when security rules allow it. Some use cases for using public subnets include web servers, external load balancers, public-facing bastion hosts. 

### Private Subnets
Private subnets does not allow public IP assignment to instances. Resources typically have only private IPs and are isolated from direct inbound internet access. Private subnets can still reach the internet for updates or outbound calls using a NAT Gateway (egress-only) or use a Service Gateway to access OCI services (like Object Storage) privately without traversing the public internet.

### Creating a Subnet:
1.

## Task 3: Different OCI Gateways: Internet, NAT, Service
Think of OCI gateways as different kinds of “doors” your cloud network (VCN) can use to reach other places. Each door has a specific purpose. In this lab, we will cover Internet, NAT, and Service gateways. These gateways are not a security control by itself—routes + security rules determine what actually gets through.

### Internet Gateways
An Internet Gateway in OCI is like the main door from your cloud network (VCN) to the public internet. You typically use an Internet Gateway for public subnets. If your subnet’s route table says “send internet traffic to the Internet Gateway,” and your instance has a public IP, then it can talk to the internet. It can also receive traffic from the internet, but only if you allow it with security rules (NSGs/security lists) and the instance/OS permits it.

### NAT Gateways
A NAT Gateway in OCI is like a one-way exit door from a private neighborhood. Your instances in a private subnet don’t have public IPs, so they can’t be reached directly from the internet.
But they still might need to go out to download updates, pull packages, or call an external API. The NAT Gateway lets them start connections out to the internet, and it “remembers” the connection so the replies can come back. People on the internet can’t start a new connection into your private instances through the NAT Gateway.

### Service Gateways
A Service Gateway in OCI is like a private tunnel from your VCN to Oracle’s cloud services (such as Object Storage), so your traffic doesn’t go out to the public internet. Your instances (often in a private subnet) can reach OCI services using private network paths. You don’t need public IPs, an Internet Gateway, or a NAT Gateway just to talk to those OCI services. It’s mainly for private, safer access to things like Object Storage, Autonomous Database endpoints.

### Creating Gateways:

## Task 4: Route Tables

### Creating Route Tables and Route Rules:

## Task 5: Security Lists & Network Security Groups

### Security Lists

### Network Security Groups

### Summary

This VCN will contain all of the other assets that you will create during this set of labs. In real-world situations, you would create multiple VCNs based on their need for access (which ports to open) and who can access them. Both of these concepts are covered in the next lab ***Create a Compute Service***.

## Acknowledgements

- **Author** - Rajeshwari Rai, Prasenjit Sarkar 
- **Contributors** - Oracle LiveLabs QA Team (Kamryn Vinson, QA Intern, Arabella Yao, Product Manager, DB Product Management)
- **Last Updated By/Date** - Sania Bolla, September 2025

