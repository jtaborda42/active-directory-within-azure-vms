<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>Preparing AD Infrastructure in Azure</h2>
<p><img width="1848" height="1982" alt="image" src="https://github.com/user-attachments/assets/15cc3537-0b0c-4c7c-bbdb-be834848fc83" />
</p>
<p>First create a resource group in Azure, we'll call it Active-Directory-Lab4. Select the appropriate subscription. For the region, I found (US) West US works for this. Afterwards, go ahead and click "review+create". You'll be taken to another window, on the bottom click "create".
</p>
<br />

<p><img width="1534" height="1508" alt="image" src="https://github.com/user-attachments/assets/5930591c-7367-415d-a655-411357473f9d" />
</p>
<p> Once your resource group has been created, click on the magnifying glass icon (this is the search bar for azure) and type in "virutal networks". Click on "virtual networks" and you will be taken to the page above. Click "create" to create your virtual network. Select the appropriate subscription, the resource group that you created, name your virtual network, and select the Region. *Make sure to select the same region as your resource group!* At the bottom, click "Review+create".

<p><img width="1680" height="1848" alt="image" src="https://github.com/user-attachments/assets/e85a8155-b2da-47cb-a46b-ccc1c7729f86" />
</p>
<p>After you click "Review+create" you should be directed to a window like the one above. Validation should have passed. Once everything looks good, click create. This will take a several minutes before we go to the next step.</p>
  
<p><img width="1866" height="1204" alt="image" src="https://github.com/user-attachments/assets/b9d627fe-2504-4593-931b-cf94a6f8fc07" />
</p>
<p>Once your resource group has been created, click on the magnifying glass icon (this is the search bar for azure) and type in "virtual machines". Click on "virtual machines" and you will be taken to the page above. Click "create" and select "virtual machine"(we will be creating two virtual machines.)</p>
<br />

<p><img width="2826" height="1924" alt="image" src="https://github.com/user-attachments/assets/5c8a3cb6-3abe-4766-aba9-07c72aac3ead" />
</p>
<p>For the first virtual machine, select your subscription and the resource group that you created. For the name of the virtual machine, we will call it "dc-2". Select the region (must be the same as your resource group and your virtual network!) For security type, select "trusted launch virtual machines". For the image, make sure to select "Windows Server 2025 Datacenter: Azure Edition x64 Gen2". </p>
<h2>High-Level Deployment and Configuration Steps</h2>

- Step 1
- Step 2
- Step 3
- Step 4

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />
