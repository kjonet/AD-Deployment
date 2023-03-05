<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-Premisis Active Directory Deployment Configuration</h1>
This will be a walkthrough tutorial on how to configure Active Directory on a virtual machine using the cloud based platform, Microsoft Azure.Active Directory is a powerful tool that can be used to manage and centralize numour dives on a network. This is a great tool to control access to resources on a large scale. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h3>Deployment and Configuration Steps</h3>

We will be creating two virtual machones for this lab. A domain controller or DC to house Active Directory and manage other PC’s on the network and a Client PC that will then join the domain. To get started, we will need an active Azure account, a resource group, a network environment. 

<h3> Step 1:</h3>

<p> On the Microsoft Azure home page, click on “Resource Gropus” and click the “Creat” button over in the top left. Name your resource group. For this lab, we will name it “ADlab1”. We can go ahead and selecte “Review + Create” at the bottom. Once everything has been validated,  select “Creat”.  A resource group is simply just a container on Azure that hold all of the resources needed for a specific group.</p>

</br>
<a href="https://imgur.com/Yb70MNB"><img src="https://i.imgur.com/Yb70MNB.png" title="source: imgur.com" /></a>
</br>

<h3> Step 2:</h3>

<p> Once the resource group has been created, we will need to set up our virtual machine. To do this, navigate back to the Azure home page by clicking “Home” in the upper top left corner. Once there, click “Virtual Machines”. Next, hit the “Creat” button and select Azure Virtual Machines from the drop down.
</br>
<a href="https://imgur.com/rKd7OqE"><img src="https://i.imgur.com/rKd7OqE.png" title="source: imgur.com" /></a>
</br>

<p>Once there, change the resource group to the one we just created, “ADlab1”. Then, name your virtual machine. For this demonstration, we’ll name it, “AD-DC” for “Active Directory Domain Controller”. Next, select the region the virtual machines server will be then select the image os. In order for AD to run, we will need to select a Windows Server Datacenter os. For this demonstration, we will use Windows Server 2016.</p>

<p> Next, address the size as needed. Windows Server 2016 needs at least 1.4 GHZ CPU and at least 2GB of RAM to run. Since this is just a small home lab, we will select the option that allows for 2 CPUS and 4 GB of RAM. 
</p>

</br>
<a href="https://imgur.com/9CoBM4V"><img src="https://i.imgur.com/9CoBM4V.png" title="source: imgur.com" /></a>
</br>



<p> Next, we will need to create administrator credentials. And afterwards, we will keep the selected port “RDP (3389)” open because we will need to connect to this VM with the use of remote desktop later. </p>
</br>

<a href="https://imgur.com/5FrHi6I"><img src="https://i.imgur.com/5FrHi6I.png" title="source: imgur.com" /></a>
Next, check off the boxes in the licesnsing section and click “Review + create”. 
</br>
Once the Dc has been created, Azure will automatically assign an ip address from their DHCP server. However, in a normal use case, a domain controller would ideally have a static address. We will eventually configure the DC’s ip address to a static later on in this walkthrough. </p>
<a href="https://imgur.com/W0i5Dml"><img src="https://i.imgur.com/W0i5Dml.png" title="source: imgur.com" /></a>
</br>



<h3> Step 2:</h3>

<p> As mentioned earlier, we have an automatic ip address assigned by Azure’s DHCP server but we want to configure that to static.  Will need to go back into our VM network settings and configure the NIC or network interface card. To do this, head back to the virtual machine we just configured and select “Networking” over in the left hand panal where it says, “Settings”. Next, select your Network Intercae card. </p>

<a href="https://imgur.com/pzwAgA8"><img src="https://i.imgur.com/pzwAgA8.png" title="source: imgur.com" /></a>
</br>
<p>Then, select “IP configurations” over to the left under “Settings”.</p>
<a href="https://imgur.com/BnVmm8r"><img src="https://i.imgur.com/BnVmm8r.png" title="source: imgur.com" /></a>
</br>

<p>Click on the table below.Here is where we will be able to configure our IP address from dynamic, to static. Go ahead and save the settings by pressing the save icon in the top left. </p>

<a href="https://imgur.com/yte9iZM"><img src="https://i.imgur.com/yte9iZM.png" title="source: imgur.com" /></a>

<h3> Step 3:</h3>

<p> Now that our DC has been configured, we will need to set up a Client-PC. To do this, the steps are essentially the same as they are for setting up the DC virtual machine. However, instead of Windows Server, we will be using Windows 10 Pro and the ip address for this VM will remain dynamic. </p>

- Windows 10 (21H2)
