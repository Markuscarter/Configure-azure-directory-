# Configure-azure-directory-

<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of  Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

-Coming Soon 

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1 Create a Resource Group 
- Step 2 Create a Virtual Network 
- Step 3 Creat a Domain Controller VM (Windows Server 2022) Named DC-1
- Step 4 After VM is created, set Domain Controller’s NIC Private IP address to be static
- Step 5 Set up Clent -1 in Azure - Creat the client VM (Windows 10) Named client-1
- Step 6 Attach it to the Same region and Virtual Netwok as DC-1
- Step 7 From Azure Portal , Restart client-1
- Step 8 Login to client-1
- Step 9 Ping the DC-1's Private IP Address
- Step 10 From the client -1 open PowerShell  and run the ipconfig/all
- Step 11 The output for the DNS setting should show DC-1's private IP adress 


<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/V2G7hj1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 1: Create a Resource Group
Log in to the Azure Portal.
Navigate to Resource Groups and click Create.
Provide a Name for the resource group (e.g., ADDeploymentGroup).
Select a Region that will host all resources (e.g., East US).
Click Review + Create, and then Create to deploy the resource group.</p>
<br />

<p>
<img src="https://i.imgur.com/v3XhUhr.png"height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 2: Create a Virtual Network
Go to Virtual Networks in the Azure Portal and click Create.
In the Basics tab, enter:
Name: ADVirtualNetwork.
Region: Same as the resource group (e.g., East US).
Associate it with the resource group created in Step 1.
Click Review + Create, then Create.
</p>
<br />

<p>
<img src="https://i.imgur.com/9jqP8hw.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 3: Create a Domain Controller VM (Windows Server 2022) Named DC-1
Navigate to Virtual Machines and click Create.
In the Basics tab:
Choose the resource group created in Step 1.
Name: Enter DC-1.
Region: Ensure it matches the virtual network's region.
Image: Select Windows Server 2022 Datacenter.
Size: Choose a size (e.g., Standard DS2_v2).
Administrator Account: Set up a username and password.
Under the Networking tab:
Select the ADVirtualNetwork created in Step 2.
Assign it to the Subnet (e.g., 10.0.0.0/24) Or leave it at default.
Click Review + Create, then Create to deploy the VM..
</p>

<p>
Step 4: Set Up Client-1 in Azure - Create the Client VM (Windows 10) Named Client-1
Navigate to Virtual Machines and click Create.
In the Basics tab:
Choose the resource group created in Step 1.
Name: Enter Client-1.
Region: Ensure it matches the region of DC-1.
Image: Select Windows 10 Pro, version 21H2.
Size: Choose a size (e.g., Standard B2s).
Administrator Account: Set up a username and password.
Under the Networking tab:
Select the ADVirtualNetwork created in Step 2.
Assign it to the Subnet (e.g., 10.0.0.0/24).
Click Review + Create, then Create to deploy the VM.

</p>
<br /><p>
<img src="https://i.imgur.com/HkusWMU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 5: After VM is Created, Set Domain Controller’s NIC Private IP Address to Be Static
Once DC-1 is deployed, navigate to Virtual Machines > DC-1 > Networking.
Under Network Interface, click the name of the network interface.
Go to IP Configurations and select the configuration (e.g., ipconfig1).
Set Assignment to Static and confirm the current private IP address.
Save the configuration.
</p>
<br /><p>
<img src="https://i.imgur.com/DZAdCDM.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 6: Attach It to the Same Region and Virtual Network as DC-1
Ensure Client-1 is associated with the same Region and ADVirtualNetwork created in Steps 1 and 2.

</p>

<p>
Step 7: From Azure Portal, Restart Client-1
Navigate to Virtual Machines > Client-1.
Click Restart to ensure all configurations are applied.
</p>
<p>
Step 8: Log In to Client-1
Use Remote Desktop (RDP) to log in to Client-1 using the credentials set during its creation.

</p>
<br /><p>
<img src="https://i.imgur.com/NqY68Wi.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 9: Ping the DC-1's Private IP Address
Open Command Prompt on Client-1.
Run the command:
ping <DC-1 Private IP>
  </p>
<br /><p>
<img src="https://i.imgur.com/F2q5Gc1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
<p>
<img src="https://i.imgur.com/qs7g2qo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
</p>
<br /><p>
<img src="https://i.imgur.com/vRzjkao.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Step 10: Switch to Client-1 and then From Client-1, Open PowerShell and Run ipconfig /all
Open PowerShell on Client-1.
Run the following command:
ipconfig /all
Check the DNS Server entry in the output:
Confirm it shows the private IP address of DC-1 (e.g., 10.0.0.4).

<br />
<p>
Step 11: The Output for the DNS Setting Should Show DC-1's Private IP Address
Verify that the DNS Server field in the ipconfig /all output matches the static private IP address of DC-1.
<br />
