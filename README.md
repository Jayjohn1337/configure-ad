<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<!-- <h2>Video Demonstration</h2> -->

<!-- - ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com) -->

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1: Setup Resources in Azure
- Step 2: Ensure Connectivity between the Client and Domain Controller
- Step 3: Install Active Directory
- Step 4: Create an Admin and Normal User Account in AD
- Step 5: Join Client-1 on your domain (mydomain.com)
- Step 6: Setup Remote Desktop for Non-Administrative Users on Client-1
- Step 7: Create Aditional Users and attempt to log into Client-1 with one of the Users

<h2>Deployment and Configuration Steps</h2>

<h3>Setup Resources in Azure</h3>

<p>
1a.Using Microsoft Azure search for "resource group" in the highlighted field in orange. Or<br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/90797d4c-0cb8-4c82-89d0-32cf65823187"/><br>

1b.If recently used/created a resource group, click the populated image as highlighted in orange.<br> 
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/ab7b689e-5d0c-49c7-bd5e-73f1c72da15a"/><br>

1c.Create a new resource group.<br> 
  <!--<img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/7088343a-0090-475b-93fb-0d3ccbc65032"/><br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/f7d1fc4f-c28c-4a43-bfef-082653dfef9e"/><br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/620c2b3c-b7b7-4b4d-a4d7-06f38a3f8954"/><br> -->

1d.Create the Domain Controller VM (Windows Server 2022) named "DC-1". *If message pop ups click on Disk-- Network-- Review+Create, wait for validation to complete then click Create.<br>
  <!--<img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/72a45546-ea6d-4103-ae7a-98625750eddf"/><br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/b5547bea-16fe-4809-92e2-145446db3c3b"/><br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/5b651d55-2a7a-4faf-b95e-beecd62fb1d9"/><br>-->

1e. Create Client VM (Windows 10) named "Client-1". Click Disk-- Network-- Review+Create, wait for validation to complete then click Create.<br>
  <!--<img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/18eb9691-33ce-4a11-8472-3a9e796a79ff"/><br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/324b4ded-65fd-4b67-b22f-47598bca2eb5"/><br> -->

1f. Set Domain Controller's NIC Private IP address to static. Go back to Virtual Machines and Click DC-1-- Networking-- Network Interface-- IP Configurations-- ipconfig-- Static.<br>
  <!--<img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/43af6eb8-ce2b-40a1-aa72-103cc11c28c7"/><br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/1943b3ef-ddf7-4108-bc34-f3939fb76db2"/><br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/8707dc5c-0c3d-4fe9-88f6-db80922c5c6a"/><br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/9dba2f89-dc2b-46c6-826c-a50c536e34d2"/><br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/a050a047-6033-454b-8fdf-c9e17a3baecf"/><br>-->
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/26adf0e0-afb4-47cd-8556-766c76ed22f8"/><br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/2bb9aef4-dd14-4b0f-8b90-a8b2653ce5b1"/><br>

</p>

<br />

<h3>Ensure Connectivity between the Client and Domain Controller</h3>

<p>
2a. Use Remote Desktop Connection app on Windows/Remote Desktop for Windows app on MacOS to log into Client-1 and ping DC-1's IP address with ping -t (perpetual ping). Ping will time out because DC-1 firewall is configured to deny ICMP traffic.<br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/2c6efb41-2eca-4abd-b599-ad4208f522ba"/>

2b. Log into Domain Controller DC-1 and enable ICMPv4 on the local Windows firewall.<br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/3cd9565e-b55f-4de5-85a5-ad1c1492f3c1"/><br>

2c. Check back at Client-1 to see ping succeed.<br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/70dd24e4-5c87-48bc-ba9e-7884d34361a8"/><br>
</p>

<br />

<h3>Install Active Directory</h3>

<p>
3a. Login to DC-1 and install Active Directory Domain Services. Then, promote as a DC: Setup a new forest as mydomain.com. Finally, restart and log back into the DC.<br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/fb732f2a-7940-4218-b364-7014242b7c32"/><br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/1d1a65c7-f06d-4094-952c-34aafb48b3d2"/><br>

3b. After Active Directory installs, return to server manager and click on the notification triangle. Then proceed to Promote this server to a domain controller. Click Next until install is available. Once installed DC will restart. When logging back into Remote Desktop, the user name is now 'mydomain\[insert user name]'. <br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/0935f8df-06af-4705-8292-83bd38754bb8"/><br>

  </p>
<br />

<h3>Create an Admin and normal User account in AD</h3>

<p>
4a.Search for <br>
  <img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/71da65f7-f536-477e-b3bb-4ff669d81f55"/>
  
</p>
<!--
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
