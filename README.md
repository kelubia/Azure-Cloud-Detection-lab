# Azure-Cloud-Detection-lab
Monitor, prioritize and remediate potential Cloud threats in real time. 

I established and managed a dedicated cloud based home laboratory environment that closely imitated the Azure cloud infrastructure. I employed various monitoring solutions and methodologies to ensure the security of Azure services and resources and prevent unauthorised activities. I designed and carried out custom attack simulations to simulate real-world cyber threats targeting Azure deployments. I also implemented advanced attack detection techniques and response mechanisms utilizing cloud-based SIEM/SOAR solutions, providing capabilities such as security analytics, threat intelligence, threat response, and more  to identify and mitigate security incidents quickly. This hands-on experience has helped me gain expertise in Azure cloud security, threat detection, and incident response. It has strengthened my commitment to upholding the integrity and resilience of cloud-based environments.

Description:

Configuring and deploying Azure resources, including Log Analytics Workspace, Virtual Machines, and Azure Sentinel, to fortify cloud security posture. 

Implementing network and virtual machine security best practices ensures robust defence against cyber threats. 

Leverage Data Connectors to integrate diverse data sources into Azure Sentinel for comprehensive analysis. 

Proficiently interpreted and utilized Windows Security Event logs, configuring associated security policies to enhance system resilience.

Demonstrate expertise in crafting advanced KQL queries to extract actionable insights from logs. 

Engineered custom analytic rules to detect and respond to Microsoft Security Events effectively. 

Utilized MITRE ATT&CK framework to meticulously map adversary tactics, techniques, and mitigation procedures, bolstering proactive threat defence strategies.

######

 MICROSOFT SENTINEL LAB NETWORK DESIGN & TOPOLOGY on Draw.io

###
Set up Azure Lab and resources in the cloud.

Create a resource group for our various resources.
-Windows 10 VM.
-Log analysis WorkSpace.
-Azure Sentinel Resource.

![1](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/cfd6da54-1a16-4531-b616-edbd75f4dda3)

Create and deploy our VM


In Azure, when you create a virtual machine, it's like creating a computer that runs on the internet. It's placed on a Virtual Network (vnet) and gets its own IP address and network interface. 

To make sure that only the right traffic goes to and from your Azure resources, you can use a Network Security Group (NSG). This is like a fancy firewall that looks at the rules you set up to decide what traffic is allowed and what's not. These rules tell the NSG which ports can be used, which protocols are okay, and which ones are not. This helps keep your resources safe and secure from bad guys trying to get in.
![2](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/0eff4bbf-a39b-460d-8eb4-d6c72b1483d8)
![2](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/662bac09-21c1-4232-b060-9b80ff604ec5)
![3](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/ce50b77a-1727-49f3-8b1f-ee27cb2fbb74)

So, my inbounds for RDP 3389 are open to anyone, which means they can access my on-premises virtual machine (VM) via Remote Desktop Protocol (RDP). But since our public IP address is out there for anyone to see, the VM is vulnerable to brute force or password spray attacks.
![4](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/68c9684d-1d91-473e-ad5b-fdfa7789152c)

To fix this, I think we should enable Just-in-Time access. That means we'll only let people access the VM when necessary and only for a limited time. We can also restrict access to certain IP addresses and roles.
![5](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/e6a6552c-2694-49ab-a1f5-d7f4bf77adbc)
![6](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/4f7ddc90-3942-4b24-a4b4-4ebefdaa9bf6)

Here's what we need to do:

1. Select "Microsoft Defender for Cloud" in the Azure Portal.
2. Click "Environment settings" and then "Cloud Infrastructure Entitlement Management (CIEM)".
3. Select our Azure Subscription from the list provided, enable all options, and hit save.
4. In the "Advanced Protection" section, click "Just-in-Time VM access" and then click "Enable JIT on VM". 
5. Select the VM we created and use the default Just-in-Time settings. RDP is listed among the ports that will be restricted. 

Once we've completed these steps, anyone who wants to connect to the VM via RDP or another management port will be restricted, and access will be based on their IP address and assigned role.

Let's update the rules in the networking tab for our VM. We need to allow RDP traffic from the IP address of our computer for a limited amount of time. To do this, search for "Microsoft Defender for Cloud" and make the necessary changes. Our Just in Time Access rules will block any attempt to establish an RDP connection from any other IP address.
![7](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/3473cdbc-a993-498d-9acc-3b335d7ab302)
![8](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/a7849132-510c-44e1-93a7-fbda7264a141)
![9](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/e8971bc9-036d-4754-a1ad-e1ebc012daa3)
![10](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/044a2129-06f8-486d-be87-0c78c5cd8551)

Collect and store log data from Azure Resources in a Log Analytics workspace created in the same resource group as the Azure Virtual Machine.
![11](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/630b27e8-7882-4fad-9888-1b23f5aa3ed2)
![12](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/adad6d42-76d7-4540-a025-62745fbf27fa)

After successfully deploying Sentinel, you can navigate to the incidents tab to monitor any incidents that may have occurred. Currently, there are no incidents available as no data is being fed into Sentinel. Therefore, the next step is to utilize data connectors to create a data collection rule that will enable us to import data from our Windows 10 VM into Sentinel. This will allow us to detect and respond to any suspicious activities or threats in our system. By setting up data connectors and data collection rules, we can ensure that Sentinel receives a steady stream of data, thereby enabling us to keep our system safe and secure.After deploying Sentinel, navigate to the incidents tab and you will notice that currently there are no incidents as no data is being fed into Sentinel. Next, we will be using data connectors to create a data collection rule to import data from our Windows 10 VM.

![13](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/1729461c-528d-444f-8fd8-c73a31b46b0a)
![14](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/f2c29d75-e74e-412e-b4dc-a81037312051)
![15](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/3511c5de-51b9-47cf-a6be-22ea2f0e9d48)
![16](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/382c04a1-c797-4b2e-8bc0-c811d443340c)
![17](https://github.com/kelubia/Azure-Cloud-Detection-lab/assets/98921903/89e5ca16-67c8-4413-b5ce-5c09f79c17cc)





