<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />


<h2>Video Demonstration</h2>

- ### [YouTube: How to Deploy on-premises Active Directory within Azure Compute](https://www.youtube.com/watch?v=AhLArPc5QrE)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Setup Environment Azure VMs (DC-1 & Client-1)
- Install Active Directory

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Setup environment in Azure (DC-1 & Client-1) 
</p>
<br />

<p>
<img width="262" alt="client 1 ping dc1" src="https://github.com/qjackson14/adazure/assets/156969011/9ab082e0-f962-46d2-a1f5-98d9075015ef">
</p>
<p>
Ping DC-1 from Client-1 using (ping 10.0.0.4 -t) watch how requests are timed out
</p>
<br />

<p><img width="616" alt="icmp rules" src="https://github.com/qjackson14/adazure/assets/156969011/885c1789-e69c-4729-808d-ff415b27ada2">
</p>
<p>
Login to DC-1 -> Start -> wf.msc -> Inbound Rules -> Protocol ICMPv4 -> Enable Rules
</p>
<br />

<p>
<img width="315" alt="pings come thru" src="https://github.com/qjackson14/adazure/assets/156969011/96335e03-7752-4391-918d-7a17e3bb2221">
</p>
<p>
Observe how DC-1 & Client-1 are now able to communicate
</p>
<br />

<p>
<img width="471" alt="add roles and features" src="https://github.com/qjackson14/adazure/assets/156969011/2292311e-8bed-4b9b-bdfb-8ae459e2f9b8">
</p>
<p>
Open Server Manager from Start menu -> Click add roles and features
</p>
<br />

<p>
<img width="231" alt="active directory domain services" src="https://github.com/qjackson14/adazure/assets/156969011/aa00ee86-16d1-4130-9fad-e78b47ff7703">
</p>
<p>
In Roles Tab Click Active Directory Domain Services -> Add Features
</p>
<br />

<p>
<img width="570" alt="mydomain com" src="https://github.com/qjackson14/adazure/assets/156969011/231fe9ec-9b32-406e-95be-ab860e095ac8">
</p>
<p>
Add New Forest -> Select domain name (for this example its just something random mydomain.com)
</p>
<br />

<p>
<img width="565" alt="dc established" src="https://github.com/qjackson14/adazure/assets/156969011/155a89a9-7378-48eb-bb9e-012197026d9d">
</p>
<p>
Dc-1 now established as Domain Controller VM will now close
</p>
<br />

<p><img width="273" alt="active directory users and computers" src="https://github.com/qjackson14/adazure/assets/156969011/6f9198a6-7a0f-4e17-a0b3-4d870019d2f2">
</p>
<p>
Login to DC-1 -> Open Server Manager -> Click Tools -> Active Directory Users and Computers
</p>
<br />

<p>
<img width="564" alt="Organizational Units" src="https://github.com/qjackson14/adazure/assets/156969011/4a74784b-4f8f-4127-9e08-2c75edecd703">
</p>
<p>
Right click mydomain -> New -> Organizational Unit -> Create Employees/Admin folder
</p>
<br />

<p>
<img width="683" alt="static private ip address" src="https://github.com/qjackson14/adazure/assets/156969011/ee754ee6-c8bf-4a5e-91b1-0615e67e676f">
</p>
<p>
Access DC-1 through Azure -> Go to Network Settings -> IPConfig -> DNS Servers -> Switch from Dynamic to Static IP so it never changes (10.0.0.4)
</p>
<br />

<p>
<img width="660" alt="dns verify" src="https://github.com/qjackson14/adazure/assets/156969011/fe2cb579-ba32-4418-9656-bb3b5d3f9130">
</p>
<p>
Verify Client-1 is one same DNS server as DC-1 (10.0.0.4) via ipconfig /all
</p>
<br />

<p>
<img width="429" alt="domain users" src="https://github.com/qjackson14/adazure/assets/156969011/ad8c75d7-ce04-42be-9076-dbcc74c330ba">
</p>
<p>
Go to Start -> Settings -> Remote Desktop -> Select Users that can remotely access this PC -> Add -> Domain Users
</p>
<br />

<p>
<img width="849" alt="powershell script" src="https://github.com/qjackson14/adazure/assets/156969011/3b024224-259b-42a8-b59e-1242b5b36c63">
</p>
<p>
Copy script -> Click Start -> Go to Powershell ISE -> Paste script -> Run Script -> Employees folder will be filled with generated names who all have Password1 set as password
</p>
<br />

<p>
<img width="303" alt="bab qipi" src="https://github.com/qjackson14/adazure/assets/156969011/881563c8-943c-4445-96cc-226c8600128e">
</p>
<p>
Pick random name & login to Client-1 using domain name and Password1
</p>
<br />

<p>
<img width="270" alt="bab qipi command prompt" src="https://github.com/qjackson14/adazure/assets/156969011/f1b6cacf-c614-4a81-b544-52a4c5a77cb9">
</p>
<p>
Pull up command prompt type "whoami" to verify that you're logged into generated name thru Client-1
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>

</p>
<br />

