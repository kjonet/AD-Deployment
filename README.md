<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-Premisis Active Directory Deployment Configuration</h1>
This will be a walkthrough tutorial on how to configure Active Directory on a virtual machine using the cloud based platform, Microsoft Azure.Active Directory is a powerful tool that can be used to manage and centralize numour dives on a network. This is a great tool to control access to resources on a large scale. <br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services


<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h3>Deployment and Configuration Steps</h3>

We will be creating two virtual machones for this lab. A domain controller or DC to house Active Directory and manage other PC’s on the network and a Client PC that will then join the domain. To get started, we will need an active Azure account, a resource group, a network environment. 

<h3> Step 1:</h3>

<p> On the Microsoft Azure home page, click on “Resource Gropus” and click the “Creat” button over in the top left. Name your resource group. For this lab, we will name it “ADlab1”. We can go ahead and selecte “Review + Create” at the bottom. Once everything has been validated,  select “Creat”.  A resource group is simply just a container on Azure that hold all of the resources needed for a specific group.</p>

</br>
<a href="https://imgur.com/KaVFsRU"><img src="https://i.imgur.com/KaVFsRU.png" title="source: imgur.com" /></a>
</br>

<h3> Step 2:</h3>

<p> Once the resource group has been created, we will need to set up our virtual machine. To do this, navigate back to the Azure home page by clicking “Home” in the upper top left corner. Once there, click “Virtual Machines”. Next, hit the “Creat” button and select Azure Virtual Machines from the drop down.
</br><a href="https://imgur.com/7uKFn8L"><img src="https://i.imgur.com/7uKFn8L.png" title="source: imgur.com" /></a>
<a href="https://imgur.com/mkWFGQJ"><img src="https://i.imgur.com/mkWFGQJ.png" title="source: imgur.com" /></a>

</br>

<p>Once there, change the resource group to the one we just created, “ADlab1”. Then, name your virtual machine. For this demonstration, we’ll name it, “AD-DC” for “Active Directory Domain Controller”. Next, select the region the virtual machines server will be then select the image os. In order for AD to run, we will need to select a Windows Server Datacenter os. For this demonstration, we will use Windows Server 2016.</p>

<p> Next, address the size as needed. Windows Server 2016 needs at least 1.4 GHZ CPU and at least 2GB of RAM to run. Since this is just a small home lab, we will select the option that allows for 2 CPUS and 4 GB of RAM. 
</p>

</br>
<a href="https://imgur.com/y8p02Et"><img src="https://i.imgur.com/y8p02Et.png" title="source: imgur.com" /></a>




<p> Next, we will need to create administrator credentials. And afterwards, we will keep the selected port “RDP (3389)” open because we will need to connect to this VM with the use of remote desktop later. </p>
</br>
<a href="https://imgur.com/t8PlMS4"><img src="https://i.imgur.com/t8PlMS4.png" title="source: imgur.com" /></a>
<a href="https://imgur.com/JQX2xBT"><img src="https://i.imgur.com/JQX2xBT.png" title="source: imgur.com" /></a>
Next, check off the boxes in the licesnsing section and click “Review + create”. 
</br>
Once the Dc has been created, Azure will automatically assign an ip address from their DHCP server. However, in a normal use case, a domain controller would ideally have a static address. We will eventually configure the DC’s ip address to a static later on in this walkthrough. </p>
<a href="https://imgur.com/5NaYUJl"><img src="https://i.imgur.com/5NaYUJl.png" title="source: imgur.com" /></a>



<h3> Step 2:</h3>

<p> As mentioned earlier, we have an automatic ip address assigned by Azure’s DHCP server but we want to configure that to static.  Will need to go back into our VM network settings and configure the NIC or network interface card. To do this, head back to the virtual machine we just configured and select “Networking” over in the left hand panal where it says, “Settings”. Next, select your Network Intercae card. </p>

<a href="https://imgur.com/pzwAgA8"><img src="https://i.imgur.com/pzwAgA8.png" title="source: imgur.com" /></a>
</br>
<p>Then, select “IP configurations” over to the left under “Settings”.</p>
<a href="https://imgur.com/BnVmm8r"><img src="https://i.imgur.com/BnVmm8r.png" title="source: imgur.com" /></a>


<p>Click on the table below.Here is where we will be able to configure our IP address from dynamic, to static. Go ahead and save the settings by pressing the save icon in the top left. </p>

<a href="https://imgur.com/yte9iZM"><img src="https://i.imgur.com/yte9iZM.png" title="source: imgur.com" /></a>

<h3> Step 3:</h3>

<p> Now that our DC has been configured, we will need to set up a Client-PC. To do this, the steps are essentially the same as they are for setting up the DC virtual machine. However, instead of Windows Server, we will be using Windows 10 Pro and the ip address for this VM will remain dynamic. </p>


<h3> Step 4:</h3>

<p> Now that the DC and Client PC’s have been setup, we can remote into them using remote desktop. However, we need to make sure both VM’s can communicate with one another. We’ll need to enable ICMPv4 in the firewall settings of the DC. To do this, go over to search in the taskbar and type in “mstsc” or “remote dsctop”  and right click it to run as an administrator. Go over to the DC virtual machine in Azure and copy the public IP address. 
To log in, we well use the log in credentials we made for the DC virtual machine first. 
Next, we will then connect to the Client PC’s remote desktop. Before we reconfigure any firewall settings, we will test to see if we receive a ping back from the DC. To test this we will use the ping command in the command prompt of the Client PC. 
<br>
Ping -t 10.2.0.4. Here we will observe that the connection will time out. This is because ICMPv4 traffic  needs to be enabled on the Domain controller. 
</br>
<a href="https://imgur.com/W5fAHgi"><img src="https://i.imgur.com/W5fAHgi.png" title="source: imgur.com" /></a>
<br>

<p>To do this, we’ll head back over to the DC. </p>


</p>

<h3> Step 5:</h3>

<p> In the DC virtual machine, type in “wf.msc” in the search bar. Right click Windows Defender Firewall and run as administrator. Next, select “Inbound Rules” and sort the data by protocol. Search for ICMPv4 and enable all ICMPv4 rules. Once enabled, navigate over to the Client PC. You should see a successful reply from the DC on the Client PC now. </p>

<a href="https://imgur.com/utIhtV9"><img src="https://i.imgur.com/utIhtV9.png" title="source: imgur.com" /></a>

<a href="https://imgur.com/l5fWILV"><img src="https://i.imgur.com/l5fWILV.png" title="source: imgur.com" /></a>



<h3> Step 6:</h3>

<p> Now that we know we can successfully ping the domain controller we can install and configure Active Directory Services on the DC. Navigate back to the DC and open “Server Manager”, then click on “Add roles and features” and turn on “Active Directory Domain Services”  and add on any additional features. Proceed to install. </p>

<a href="https://imgur.com/QcN5Ai7"><img src="https://i.imgur.com/QcN5Ai7.png" title="source: imgur.com" /></a>


<p> Once Active Directory has been installed, we will need to turn the server into a domain controller. To do this, navigate to the flag at the top and click “Promote this server to a domain controller”. </p>

<a href="https://imgur.com/koxt8ql"><img src="https://i.imgur.com/koxt8ql.png" title="source: imgur.com" /></a>

<p>At the Deployment Configuration window, you’ll want to select “Add a new forrest” and create a root domain name. For this lab, we’ll call it “mydomain.com”. Select next, and set up a DSRM password. Next, proceed with the rest of the installation. Once everything is installed, you’ll need to restar the DC VM and log back in. </p>

<h3> Step 7:</h3>

<p>Once the DC VM has restarted, you’ll log in remotely by using  mydomain.com\user. This is necessary now that are domain controller is active. Next, proceed to type in the usual password.  </p>

<h3> Step 8:</h3>

<p>Now that Active Directory is running, we can creat a few Orginizational Units or OU’s. To do this, go to tools and select Active Directory Users and Coputers. Navigate to mydomain.com over to the left. We will create two Organizational Units named “_EMPLOYEES” and the other “_ADMINS”</p>


<a href="https://imgur.com/kuTbUVB"><img src="https://i.imgur.com/kuTbUVB.png" title="source: imgur.com" /></a>

<a href="https://imgur.com/LjxUzbD"><img src="https://i.imgur.com/LjxUzbD.png" title="source: imgur.com" /></a>

<p> Aftwards, we can proceed to creat a new admin in the “_ADMINS_” folder. For this lab, we will call her Jane Doe. We’ll give her a user name of “JDoe” select next and setup a password. Uncheck, uncheck "User must change password at next logon". </p>

<a href="https://imgur.com/arbC79b"><img src="https://i.imgur.com/arbC79b.png" title="source: imgur.com" /></a>


<h3> Step 8:</h3>

<p> Now that we have a new admin, we can adjust her permissions. We want to add Jane to the Domain Admin. To do that, we’ll need to right click her name and go to Properties. Then, select Member Of and Add. Type “Domain” in the object box, then hit Check Names. Select Domain Admins and hit OK and then Apply. We will then proceed to logout of the DC VM and log back in as Jane Doe. </p>

<a href="https://imgur.com/X4WlBUN"><img src="https://i.imgur.com/X4WlBUN.png" title="source: imgur.com" /></a>

<a href="https://imgur.com/Vf0iXM9"><img src="https://i.imgur.com/Vf0iXM9.png" title="source: imgur.com" /></a>

<h3> Step 9:</h3>

<p> Next, we’ll need to configure the Clint-PC’s DNS server to the private IP address of the DC. This will allow the Client PC to be joined to mydomain.com. To do this, go to the Azure portal. Select the virtual machine for the Client PC. Select Networking under Settings. Afterwards, click the Clint PC’s NIC. Then, over to the left, under setting, select DNS servers. Select custom and type in the private ip address of the DC virtual machine. Save it and restart the Client PC from the Azure portal. </p>

<a href="https://imgur.com/nDiZv1b"><img src="https://i.imgur.com/nDiZv1b.png" title="source: imgur.com" /></a>

<h3> Step 10:</h3>

<p> Log back into the Client PC and go over the start menu, right click, and select Settings. From there, select System, About, and select “Rename this PC (advanced)” . Click “Change” and select the domain radio button. Type in “mydomain.com” and click OK. There, a log in window will appear, this is where you will type in the credentials of your admin user. Select OK and a prompt should appear notifying you that you have successfully connected to the domain. </p>
<a href="https://imgur.com/6BGE33g"><img src="https://i.imgur.com/6BGE33g.png" title="source: imgur.com" /></a>

<a href="https://imgur.com/bPOUIZX"><img src="https://i.imgur.com/bPOUIZX.png" title="source: imgur.com" /></a>

<a href="https://imgur.com/PLJ4Vef"><img src="https://i.imgur.com/PLJ4Vef.png" title="source: imgur.com" /></a>



