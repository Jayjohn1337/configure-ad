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

<p>
<!--<img src="https://github.com/Jayjohn1337/configure-ad/assets/67848718/a6acbd78-a00d-4796-b4f3-76002f408e93"/>-->
</p>
<!--<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<!--
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
