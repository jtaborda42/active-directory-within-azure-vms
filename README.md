<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the preparation of a client server and domain controller through virtual machines and the implementation of on-premises Active Directory within Azure Virtual Machines.<br />

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
<p>Step 1: create a resource group, we'll call it Active-Directory-Lab4. Select the appropriate subscription. For the region, I found (US) West US works for this. Afterwards, go ahead and click "review+create". You'll be taken to another window, on the bottom click "create".
</p>
<br />

<p><img width="1534" height="1508" alt="image" src="https://github.com/user-attachments/assets/5930591c-7367-415d-a655-411357473f9d" />
</p>
<p> Click on the magnifying glass icon (this is the search bar for azure) and type in "virutal networks". Click on "virtual networks" and you will be taken to the page above. Click "create" to create your virtual network. Select the appropriate subscription, the resource group that you created, name your virtual network, and select the Region. *Make sure to select the same region as your resource group!* At the bottom, click "Review+create".

<p><img width="1680" height="1848" alt="image" src="https://github.com/user-attachments/assets/e85a8155-b2da-47cb-a46b-ccc1c7729f86" />
</p>
<p>After you click "Review+create" you should be directed to a window like the one above. Validation should have passed. Once everything looks good, click create. This will take a several minutes before we go to the next step.</p>
  
<p><img width="1866" height="1204" alt="image" src="https://github.com/user-attachments/assets/b9d627fe-2504-4593-931b-cf94a6f8fc07" />
</p>
<p>Once your resource group has been created, click on the magnifying glass icon (this is the search bar for azure) and type in "virtual machines". Click on "virtual machines" and you will be taken to the page above. Click "create" and select "virtual machine"(we will be creating two virtual machines.)</p>
<br />

<p><img width="2826" height="1924" alt="image" src="https://github.com/user-attachments/assets/5c8a3cb6-3abe-4766-aba9-07c72aac3ead" />
</p>
<p>For the first virtual machine, select your subscription and the resource group that you created. For the name of the virtual machine, we will call it "dc-2". Select the region (must be the same as your resource group and your virtual network!) For security type, select "trusted launch virtual machines". For the image, make sure to select "Windows Server 2025 Datacenter: Azure Edition x64 Gen2". The size should be "Standard_D2s_v3 - 2 vcpus, 8 GiB memory. Note: Don't stress too much about the cost, this is if the virtual machine is left running for hours on end. We will show you how to turn the virtual machine off so it doesn't rack up on your account.</p>
<br />

<p><img width="3108" height="1578" alt="image" src="https://github.com/user-attachments/assets/76979ea9-9f84-4b15-8513-74e3e447ae5a" />
</p>
<p> Scroll down the page and you should see the next section that says "Administrator account". For the username, we can use "labuser" and choose the password of your choice. Good rule of thumb: Capital letter, lowercase letters, numbers, and special characters help create a strong password. For public inbound ports, "allow selected ports". For select inbound ports, select "RDP (3389)". Check both boxes for the licensing and then click "Next:Disks" and click "Next: Networking".</p>
<br />

<p><img width="3058" height="1998" alt="image" src="https://github.com/user-attachments/assets/622c9c48-e6cd-4a33-a2dd-4fff0a8d535c" />
</p>
<p>For your virtual network, make sure to select the virtual network that we created called "Active-Directory-VNet". The subnet bar should be "default (10.0.0.0/24). For your public IP, make sure to select "dc-2-ip". NIC network seciruty group should be "basic. Public inbound ports should be "allow selected ports". Inbound ports should be "RDP (3389). Check "Enable accelerating networking" and load balancing options can be left as "none". Go ahead and click "Review+create". Once the window loads, click "create". The first virtual machine will take some time to deploy, about several minutes. </p>
<br />

<p><img width="2452" height="1860" alt="image" src="https://github.com/user-attachments/assets/50a090c8-d315-45e4-992a-0e12c9762fcb" />
</p>
<p>Once your first virtual machine has successfully deployed, go ahead and go back to "virtual machines" in the search bar. We're going to create the second virtual machine. Same process, select the appropriate subscription (the subscription should be the same as your resource group, virtual network, and your first virtual machine). Resource group, select the resource group we created, in this case "active-directory-lab". The name of your second virtual machine will be "client-2". Set the region as your resource group and virtual machine, in this case "(US) West US". Availability options should be "no infrastructure redunandcy required". Security type, "trusted launch virtual machines."</p>
<p>*For your image, select "Windows 11 Pro, version 25H2 - x64 Gen2". VM architecture should be "x64". The size should be "Standard_D2s_v3 - 2 vcpus, 8 GiB memory."</p>
<br />

<p><img width="2162" height="2018" alt="image" src="https://github.com/user-attachments/assets/c68c3410-9f80-4447-8c2f-c65a4ab147ad" />
</p> 
<p>Username, we will use the same username as the first virtual machine; in this case, "labuser". Password can be the same as your first virtual machine *be sure to write down the username(s) and password(s) in case you forget!* On Public inbound ports, select "allow selected ports". Select "RDP (3389)" for inbound ports. Check the licensing box and click "next: disks" and then "next: networking".</p>
<br />

<p><img width="2336" height="1980" alt="image" src="https://github.com/user-attachments/assets/a3febe52-d813-4f82-af5c-fdc4aeb770b6" />
</p>
<p> On the "network interface" section, select "active-directory-VNet" for your virtual network. Subnet, Public IP, NIC network security group, Public inbound ports, inbound ports should be the same as the above picture. Then go ahead and click "Review+create". Once the window loads, click "create" and the second virtual machine should deploy. Again, it will take a couple minutes to complete.</p>
<br />

<p><img width="2942" height="1884" alt="image" src="https://github.com/user-attachments/assets/bec5485c-3d2a-439c-a2b1-e4d6402ad40f" />
</p>
<p>Once the "client-2" virtual machine is loaded, go back to the search bar and select "virtual machines". Click on the "dc" virtual machine. On the drop down menu (underneath the search bar and overview on the left), open the "networking" tab and click on "network settings". Here, we are going to change the private IP address from "dynamic" to "static". This is so the client-1 virtual machine communicates with the dc virtual machine without the private IP address continously changing. </p>
<br />

<p><img width="4062" height="2010" alt="image" src="https://github.com/user-attachments/assets/ba268bd1-db56-4b3f-83a2-5a69a23a7b4d" />
</p>
<p>You should be able to see a small window in "network settings" that says "Network interface / IP configuration: dc-2589 (primary) / ipconfig1 (primary)" click on the blue lettering and it will take you to the next window.</p>
<br />

<p><img width="2918" height="1548" alt="image" src="https://github.com/user-attachments/assets/58a84815-f73e-4e48-9298-2c040183a838" />
</p>
<p>Here you will be on the "IP configurations" settings. Click on the blue lettering that says "ipconfig1". It will open another window that says "edit IP configuration."</p>
<br />

<p><img width="4096" height="2056" alt="image" src="https://github.com/user-attachments/assets/2001864b-f706-46db-b6ab-93f17d87abc7" />
</p>
<p>Under "Private IP address settings", you should see the "Allocation" section with the options "dynamic or static". Select "static" and then click the blue "save" button below. This will keep the private IP address for the dc virtual machine the same, always.</p>
<br />

<p><img width="2930" height="2058" alt="image" src="https://github.com/user-attachments/assets/9b7521fe-a207-4d21-b3c7-16a62989f394" />
</p>
<p>Now go back to the "dc" virtual machine. We're going to copy the public (not the private) IP address. In the "overview" tab, you should see the window above. On the right hand side of the screen, you should see "Primary NIC public IP". Hover your mouse over the public IP address and there should be an icon that pops up next to the IP address. Click on that icon to copy the IP address to your clipboard.</p>
<br />

<p><img width="2352" height="1236" alt="image" src="https://github.com/user-attachments/assets/fcabe270-3887-442b-b618-2f62f7ea3950" />
</p>
<p>Open the app store on your desktop and search for "windows app". (On Mac, this is previously known as 'Remote Desktop'. This is how we will be launching the virtual machines.) Open "Windows App". (For non-Mac users, the common app is 'Remote Desktop Connection')</p>
<br />

<p><img width="2016" height="1430" alt="image" src="https://github.com/user-attachments/assets/9ee19084-c871-40f3-8b56-18e96b0d2898" />
</p>
<p>Once Windows App (or Remote Desktop Connection) is open, click on the '+' sign and select "add PC". </p>
<br />

<p><img width="1878" height="1438" alt="image" src="https://github.com/user-attachments/assets/c4bf598b-af2b-4e7d-bc5b-6b5e112d088a" />
</p>
<p>Paste the public IP address for the dc virtual machine in the "PC name" tab. In the 'friendly name' tab, type in "dc-2" and click on "add". </p>
<br />

<p><img width="1556" height="1094" alt="image" src="https://github.com/user-attachments/assets/7caee27a-2c44-49e7-be8e-bdee2e94bb3a" />
</p>
<p> If entered correctly, you should see the 'dc-2' virtual machine in saved devices. Go ahead and double click on "dc-2" and a window will pop up asking you to input your credentials. Type in the username 'labuser' and the password you set for the virtual machine. Click 'connect' and another window will pop up. Click connect again and you should be connected to the dc-2 virtual machine.</p>
<br />

<p><img width="4096" height="2210" alt="image" src="https://github.com/user-attachments/assets/8e5f6b2b-d644-43db-a0ae-55a82d523844" />
</p>
<p>Once the virtual machine has loaded, you will know that you connected to the dc-2 virtual machine if the systems manager window pops up as the machine loads. If this window does not automatically pop up, there was an error made during the set up process. For this next step, we're going to turn off the firewall in the virtual machine (just for the sake of the lab only).</p>
<br />

<p><img width="1646" height="1322" alt="image" src="https://github.com/user-attachments/assets/99c774d2-704b-4eae-8ded-ee65c5e9ff89" />
</p>
<p>Right click on the start menu (the windows icon) and you should see a menu pop up. Click on "Run".</p>
<br />

<p><img width="1274" height="550" alt="image" src="https://github.com/user-attachments/assets/e5b52416-2cb0-4442-8011-0ab8ca2c1f96" />
</p>
<p>In the open bar, type in "wf.msc" and click OK.
</p>
<br />

<p><img width="2922" height="1674" alt="image" src="https://github.com/user-attachments/assets/e8d006cc-09b0-4bcc-855a-3dfdfca7f039" />
</p>
<p>Click on "Windows Defender Firewall Properties" and a second window should open. Under the "Domain Profile" tab, turn off the firewall. Do the same for the "Private Profile" tab and the "Public Profile" tab. Once all three firewalls are turned off, click "apply" and then click "ok".</p>
<br />

<p><img width="3596" height="2092" alt="image" src="https://github.com/user-attachments/assets/5a6e8b23-c059-454c-ad78-394bce9c1f38" />
</p>
<p>Next we're going to set Client-2's DNS settings to DC-2's Private IP address. Go back to virtual machines in azure and click on DC-2. You should be able to see the overview section of DC-2. DC-2's private IP address in this case is 10.0.0.4. Yours might be different, just bare in mind.  </p>
<br />

<p><img width="2450" height="1894" alt="image" src="https://github.com/user-attachments/assets/253f5493-01dc-49b4-8080-c9593a78cd38" />
</p>
<p>Go back to virtual machines, click on "Client-2". On the left hand side, you should see various tabs. Look for the one that says "Networking" and click on it. There should be a few more tabs, click on the one that says "Network Settings". Next, click on the Network Interface Card (client-2921 (primary) / ipconfig1 (primary).</p>
<br />

<p><img width="2320" height="1488" alt="image" src="https://github.com/user-attachments/assets/57aa91ac-924e-4435-aacf-8731dade741e" />
</p>
<p>On the left hand side, you should see several options under "Settings". Click on the option that says "DNS servers". Switch the DNS server to "Custom" and in the box that says "add DNS server", type in the private IP address for DC-2. Make sure to hit "Save" (next to the discard button). </p>
<br />

<p><img width="3836" height="1362" alt="image" src="https://github.com/user-attachments/assets/7ffe35c2-9fed-4162-bf1b-e64f0e7912cf" />
</p>
<p>Go back to the virtual machines section, check the box next to "client-2" and click "restart". You'll have a window pop up confirming to restart the selected virtual machines. Click yes or ok. Give it a few minutes and then log back in on the Windows App.</p>
<br />

<p><img width="2018" height="1434" alt="image" src="https://github.com/user-attachments/assets/3a216dc9-84b6-4d71-8a86-6cd448e7e474" />
</p>
<p>Go back to virtual machines in Azure and click on "client-2". Copy Client-2's public (not private) IP Address. Open the windows app. Click the "+" sign and add a computer. Paste client-2's public IP address in the PC name tab and name your computer "client-2". Click add. Now login to client-2. Remember, username is labuser and your selected password.</p>
<br />

<p><img width="2020" height="1678" alt="image" src="https://github.com/user-attachments/assets/6ec859da-f529-4426-b5dc-4bb33733d26c" />
</p>
<p>Now that we are logged into client-2, we're going to attempt to ping the private IP address of DC-2. In the search bar at the bottom, type in 'powershell' and click on "Windows Powershell" when it appears in the search bar. </p>
<br />

<p><img width="2360" height="1462" alt="image" src="https://github.com/user-attachments/assets/fdc55e96-2416-482b-bb08-adfd44159db7" />
</p>
<p>In powershell, type "ping" (ping should be in yellow), press the space bar and then type in (or paste) the private IP Address for dc-2. Hit the enter, or return, button and you should be communicating with DC-2's Private IP address. If you are not, there was an error made in the previous steps. </p>

<p><img width="3822" height="1962" alt="image" src="https://github.com/user-attachments/assets/e6d4fbb5-eb4f-48dd-b523-cf941d19abfa" />
</p>
<p>Go to your DC desktop and open "Server Manager". Click on "Add Roles and Features." Click "Next" until you reach the "Server Roles" tab. Check the box that says "Active Directory Domain Services" and click "next" until you reach the "Confirmation" tab. Check the box that says "Restart the destination server", another window will pop up with a 'yes' or 'no' option. Click yes and then click "Install."</p>


<h2>Deployment and Configuration Steps</h2>
 
