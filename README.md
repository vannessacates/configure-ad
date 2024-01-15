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

<h2>High-Level Deployment and Configuration Steps</h2>

- Create two Azure Virtual Machines (VMs) one for the Domain Controller and the other for the Client *Ensure both VMs are in the same Vnet
- Set Domain Controller’s NIC Private IP address to be static
- Ensure connectivity between the Client and Domain Controller. Do this by enabling ICMPv4 on the local windows Firewall. Ping should succeed to client.

<h2>Deployment and Configuration Steps</h2>

<p>

- Login to Domain Controller and install Active Directory Domain Services
- Promote as a DC: Setup a new forest as examplemydomain.com (can be anything, just remember what it is!)
- Restart and then log back into Domain Controller as user: examplemydomain.com\(whatever your username was that you created)

</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/5b19a536-295b-4ceb-9cfb-ff3b7a80f18d"/>
</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/acdcbe8f-7484-4f1f-9c2b-b1c826804d16"/>
</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/e45dcb42-c780-459b-845d-67b1d1c6716c"/>
</p>
<br />

<p>

- In Active Directory Users and Computers (ADUC), create an Organizational Unit (OU) called “_EMPLOYEES”
- Create a new OU named “_ADMINS”
- Create a new employee named “Jane Doe” (same password) with the username of “jane_admin”
- Add jane_admin to the “Domain Admins” Security Group. Don't forget to hit Apply!
- Log out/close the Remote Desktop connection to Domain Controller and log back in as “mydomain.com\jane_admin”
- User jane_admin as your admin account from now on

</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/ed75df6a-fd30-4842-ad3f-4d22b79ffaf6"/>
</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/54ced333-455d-4207-a741-bf9e363f5c06"/>
</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/ea6f4c58-cd79-4dbf-8155-df46b620f6e0"/>
</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/71a95797-ac98-4a03-9dd8-0a4db59909e1"/>
</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/63e7be67-9bae-4244-87da-24d3a040eab3"/>
</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/a7bb41bc-4b1f-4155-b439-200229883afa"/>
</p>
<br />

<p>

- From the Azure Portal, set Client’s DNS settings to the DC’s Private IP address
- From the Azure Portal, restart Client
- Login to Client(Remote Desktop) as the original local admin (your username you created) and join it to the domain (computer will restart)

</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/dba35ed5-aabd-4d5f-8a2a-27f25171ed87"/>
</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/16c2cd6e-bcbf-4ef6-8e64-3bb3eb1f3ecd"/>
</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/fc3c0aa4-420e-4a8b-a017-3054a4c196c2"/>
</p>
<br />

<p>

- Log into Client as mydomain.com\jane_admin and open system properties
- Click “Remote Desktop”
- Allow “domain users” access to remote desktop
- You can now log into Client as a normal, non-administrative user now
- Normally you’d want to do this with Group Policy that allows you to change MANY systems at once

</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/a5a289b2-cc0d-4688-acbe-b5a31ae17329"/>
</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/8d274a35-4aa0-4b27-a8be-8c762cb03aad"/>
</p>
<br />

<p>

- Login to Domain Controller as jane_admin
- Open PowerShell_ise as an administrator
- Create a new File and paste the contents of the script into it (https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1)
- Run the script and observe the accounts being created
- When finished, open ADUC and observe the accounts in the appropriate OU
- Attempt to log into Client with one of the accounts (take note of the password in the script)

</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/4ffead8f-8a07-4f80-ba92-7a8740494509"/>
</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/97882f40-6444-4af5-9718-b47217a4d472"/>
</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/a92de5f1-9cd2-4b79-b054-652eadfb9399"/>
</p>
<p>
<img src="https://github.com/vannessacates/configure-ad/assets/140145473/3829af5d-f3c7-4642-91b5-6f7b81986e67"/>
</p>
<br />
