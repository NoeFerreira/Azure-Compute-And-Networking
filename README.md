<p a href="center">
<h1>Azure Virtual Machines and Network Security Groups (NSGs)</h1>

In this tutorial, we’ll examine network traffic to and from Azure Virtual Machines using Wireshark, and also explore how Network Security Groups work through some hands-on examples.

<h2>Environments and Technologies Used</h2>

. Microsoft Azure (Virtual Machines/Compute)<br>
. Remote Desktop<br>
. Various Command-Line Tools<br>
. Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)<br>
. Wireshark (Protocol Analyzer)<br>

<h2>Operating Systems Used</h2>

. Windows 10 (22H2)<br>
. Ubuntu Server 24.04<br>

<h2>High-Level Steps</h2>

1.) Create Virtual Machines in Azure.<br>
2.) Observe ICMP traffic between Virtual Machines using Wireshark.<br>
3.) Configure a Firewall (Network Security Group) and analyze its impact on network traffic.<br>
4.) Observe various protocol traffic (SSH, DHCP, DNS, RDP) using Wireshark.<br>

<h1>Part 1: Create Virtual Machines</h1>

**1.) Log in to** [Azure Portal](https://login.microsoftonline.com/organizations/oauth2/v2.0/authorize?redirect_uri=https%3A%2F%2Fportal.azure.com%2Fsignin%2Findex%2F&response_type=code%20id_token&scope=https%3A%2F%2Fmanagement.core.windows.net%2F%2Fuser_impersonation%20openid%20email%20profile&state=OpenIdConnect.AuthenticationProperties%3DsON0-jai790krMrk21_Iv00mcVrZMD9IluvQsz4ZaM_ME3UhhsSJDdicez-VakjcBZT6tvONzrOONCsEJ869d0aq4h3csgSc-aQucgurg4vKJ2fFjreFwH8Db9FSfKK_s0JDsksDw3hg6w4dVGq334ep-xpGRUQpH0HS-q1-8G_qw4aRHRDgEr7qNiuy50wiXWmO7wRp_ZkowxtAgF4eM2NqhhE_7cCshQE0KeDySHSfgqiCL0E9s4iLe1Vvx8_iiZQMebtqxAk8tuIRgoBPr98E-WMA8ypfJ1HrGhu64KInNuUD8_5QDWTVMA78ibHwHykZQV0gGGKGxPA5loeORTx9vyvFDwMhKOIdpOuoq2UJoayNdmm8iOQ83DmDcJFrLsAzQzyz6A7OO1HpyaLGuZaagOr5kb-MBQG6LHKNFoRmadMeHtBBjIeD59MNIX8kzrZ4auC6GELoCTROykYXu1jr5A9Eg2lc3I7RB5smBng1cY_p_CgWx4pYCONpvJNFpjuTPArXlpUWMYjGbJppYIR4Sk5teGFO5ecxFzw9mjZH3fPLshtVxtyZv19HxXvp&response_mode=form_post&nonce=638802648691811339.ZWJhMDIxZjItZDk4Mi00ZGQ2LTg0ZjAtN2RjYjFmMDk1MmNjNzY0OTI0NzctNzQxZS00ZmNkLThmMWYtNzU5ZGFjMGNlMTA1&client_id=c44b4083-3bb0-49c1-b47d-974e53cbdf3c&site_id=501430&client-request-id=efd57589-611a-40f4-90a8-546352cf44ff&x-client-SKU=ID_NET472&x-client-ver=8.3.0.0)<br>

**2.) Create a Resource Group**:<br />
. Navigate to "Resource Groups" and click "Create."<br>
. Provide a name for your Resource Group and select a region.<br>
. Click "Review + Create," then "Create."<br>
![image](https://github.com/user-attachments/assets/cf81442b-01bc-4f9a-be7f-3a7025745ea7)

**3.) Create a Windows 10 Virtual Machine**:<br>
. Navigate to "Virtual Machines" and click "Create."<br>
. Select the Resource Group you just created.<br>
. Configure the Virtual Machine:<br>
- OS: Windows 10<br>
- Create username and password<br>
- Head to the Networking section, then create a new virtual network titled "Lab-vnet"<br>
. Complete the setup and deploy the VM.<br>

![image](https://github.com/user-attachments/assets/af3080ba-e9ff-4738-9612-a9b4fdcdbc3b)
![image](https://github.com/user-attachments/assets/afb9e36c-dbf0-40db-9a95-9e326b5cfcb5)
![image](https://github.com/user-attachments/assets/bd5f8054-c557-4fb6-b0a6-1cbfc0e68c3a)


**4.) Create a Linux (Ubuntu) Virtual Machine**:<br />
. Navigate to "Virtual Machines" and click "Create."<br>
. Select the same Resource Group and Virtual Network used for the Windows 10 VM.<br>
. Configure the Virtual Machine:<br>
- OS: Ubuntu Server 24.04<br>
- Authentication: Username/Password.<br>
. Ensure both VMs are in the same Virtual Network and Subnet as the Windows 10 VM.<br>
. Complete the setup and deploy the VM.<br>

![image](https://github.com/user-attachments/assets/a5b73220-70a4-47ff-bcf5-e2c209452c3f)
![image](https://github.com/user-attachments/assets/617a397b-b039-463c-82e8-ed9d32015e79)
![image](https://github.com/user-attachments/assets/c83bc41d-31d6-48e5-883d-d47c60d2edfd)
![image](https://github.com/user-attachments/assets/c9fc3802-4885-458d-bed2-da22f77710af)

<h1>Part 2: Observe ICMP Traffic</h1>

**1.) Use Microsoft Remote Desktop to connect to your Windows 10 Virtual Machine (if on Mac, install the client first)**.<br />

**2.) Install Wireshark on the Windows 10 VM**:<br>
- Download and install [Wireshark](https://www.wireshark.org)<br />

**3.)Open Wireshark and start a packet capture.**<br>

**4.) Filter for ICMP traffic in Wireshark.**<br>

**5.)Retrieve the private IP address of the Ubuntu VM and attempt to ping it from the Windows 10 VM**:<br>
- Open Command Prompt or PowerShell and run: *ping Ubuntu VM Private IP* .<br>
- Observe the ping requests and replies in Wireshark.<br>

**6.)From the Windows 10 VM, ping a public website (e.g., www.google.com) and observe the ICMP traffic in Wireshark.**<br>

![image](https://github.com/user-attachments/assets/66270e75-c391-4900-9be1-660c1e7ed915)

<h1>Part 3: Configure a Firewall (Network Security Group)</h1>
<h2>Observe ICMP Traffic with Firewall Changes</h2>

1.) Initiate a continuous ping from your Windows 10 VM to the Ubuntu VM:<br>
- Command: ping Ubuntu VM Private IP -t.<br>

2.) Open the Network Security Group associated with the Ubuntu VM.<br>
3.) Disable inbound ICMP traffic in the Network Security Group.<br>
4.) Observe the ICMP traffic in Wireshark and the command line Ping activity (should stop).<br>
5.) Re-enable ICMP traffic in the Network Security Group.<br>
6.) Observe the ICMP traffic in Wireshark and the command line Ping activity (should resume).<br>
7.) Stop the ping activity.<br />

![image](https://github.com/user-attachments/assets/54114a74-5b25-467f-a108-0964c0ea7fd5)
![image](https://github.com/user-attachments/assets/d7b0ed13-1b56-4b90-8009-734f9a07e121)
![image](https://github.com/user-attachments/assets/eeb48e27-09ba-4912-ab32-c3d8a68259f0)
![image](https://github.com/user-attachments/assets/3d83b410-11df-4423-85e8-a4ebaea4b11d)
![image](https://github.com/user-attachments/assets/d8a6484d-ddca-4ca2-8bb4-4532026908a4)

<h2>Observe SSH Traffic</h2>

1.) In Wireshark, start a new packet capture and filter for SSH traffic.<br>
2.) From the Windows 10 VM, SSH into the Ubuntu VM:<br>
- Command: ssh <username>@<Ubuntu VM Private IP.<br>
- Enter the password when prompted (the password will not be visible).<br>

3.) Type commands within the SSH session and observe the SSH traffic in Wireshark.<br>
4.) Exit the SSH session: exit.<br>

![image](https://github.com/user-attachments/assets/c3136ee4-321b-47ac-ac23-8274220aa9b8)
![image](https://github.com/user-attachments/assets/542f9f57-f45c-466b-8f96-80471e9bbd2f)
![image](https://github.com/user-attachments/assets/57b5d7bf-0af2-43f7-9a1b-21b635f60d47)

<h2>Observe DHCP Traffic</h2>

1.) In Wireshark, filter for DHCP traffic.<br>
2.) From the Windows 10 VM, issue a new IP address:<br>
- Open PowerShell as admin and run: ipconfig /renew.<br>

3.) Observe the DHCP traffic in Wireshark.<br>
4.)In this case our vm maintains the same IP. If we were to release our IP address (ipconfig /release) then renew it (ipconfig /renew) we would see the complete DHCP cycle in wireshark.<br>

![image](https://github.com/user-attachments/assets/7dfce655-f4fe-4ecf-b12d-7737116e855e)

<h3>Observing the full DHCP Cycle</h3>
. Open notepad and type the release and renew commands<br>
. Choose a location to save the program. Here we chose c:\program data (in my case, I put c:\) <br> 
. You can name the file whatever you want but make sure to save it as a .bat file (this turns it into a simple script that we can run)<br>
. Make sure to change the 'save as type' to all files<br>

![image](https://github.com/user-attachments/assets/0a0ea47c-cd73-40df-87c1-9bb897af2f6c)

. Change the directory that PowerShell is accessing to the location of the your .bat file by entering 'cd c:(filelocation)'<br>
. In this case I will change the directory to c:\programdata<br>
. Run the DHCP.bat script that was just created by entering '.\dhcp.bat'<br>
. This program should temporarily disconnect you from the vm because the IPv4 address is being released and renewed<br>
. Observe the Release - Discover - Offer - Request - Acknowledge steps in the DHCP process<br>
![image](https://github.com/user-attachments/assets/d2268b1f-3ae0-4b22-a5a5-51538693763f)

<h3>Observe DNS Traffic</h3>

1.) In Wireshark, filter for DNS traffic.<br>
2.) From the Windows 10 VM, use nslookup to find IP addresses for websites:<br>
- Example: nslookup disney.com.<br>

3.) Observe the DNS traffic in Wireshark.<br>

![image](https://github.com/user-attachments/assets/5c3cea50-b755-41ca-ac4d-e1efaf4aa971)

<h3>Observe RDP Traffic</h3>

1.) In Wireshark, filter for RDP traffic:<br>
- Use the filter: tcp.port == 3389.<br>

2.) Observe the continuous RDP traffic between the Windows 10 VM and your local machine.<br>

![image](https://github.com/user-attachments/assets/642d97e1-d8fe-42df-a1c7-8c8a6da9be7f)
