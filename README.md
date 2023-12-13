<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

<h1>osTicket - Prerequisites and Installation</h1>
This tutorial outlines the prerequisites and installation of the open-source help desk ticketing system osTicket.<br />

<h2>List of Prerequisites</h2>
<ul>
<li>Enable IIS</li>
<li>Install Web Platform Installer</li>
<li>Install MYSQL and setup username and password</li>
<li>Install Microsoft Visual C++ 2009 Redistributable Package</li>
<li>Configure permissions and install osTicket</li>
</ul>

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Computers)
- Remote Desktop
- Internet Information Services (IIS)
- osTicket (open source ticketing system)

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)

<h2>Installation Steps </h2>

- Create a Virtual Machine (VM) in Azure by going to portal.azure.com and creating an account.
- Then create a resource group and a Windows 10 Virtual Machine (VM) with 2-4 Virtual CPUs (vcpus) and allow it to create a new Virtual Network (Vnet)

  ![image](https://github.com/ArmandiJ/osTicket-Prerequisites-and-Installation/assets/153237878/7bf2413b-383c-4732-87ee-70c5cad52726)

- Using the VM's public IP address connect to the VM through remote desktop connection (Microsoft Remote Desktop if you're on a Mac)
- At bottom left search for control panel
- Underneath Programs, select Uninstall a Program
- Select Turn Windows Features On or Off
- Enable Internet Information Services (IIS) World Wide Web Services -> Application Development Features ->
[X] CGI
[X] Common HTTP Features
- AND IIS Management Console
Internet Information Services -> Web Management Tools -> IIS Management Console

![image](https://github.com/ArmandiJ/osTicket-Prerequisites-and-Installation/assets/153237878/269ebd83-8737-413b-b7ed-85e8a4d7d8c2)

- Next download and install PHP Manager for IIS (PHPManagerForIIS_V1.5.0.msi)
- Download and install the Rewrite Module (rewrite_amd64_en-US.msi)
- Go to "This PC" or "My Computer" then to the C driver (C:\\) and create the directory C:\PHP (create a folder and name it PHP) 
- Download PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) and unzip or extract the contents into C:\PHP
- Download and install VC_redist.x86.exe
- Download and install MySQL 5.5.62 (mysql-5.5.62-win32.msi)  Typical Setup -> Launch Configuration Wizard (after install) -> Standard Configuration -> Create a password
- Open IIS as an Admin

![image](https://github.com/ArmandiJ/osTicket-Prerequisites-and-Installation/assets/153237878/b3283d31-b508-406c-a675-01d2b212592b)

- Register PHP from within IIS
![image](https://github.com/ArmandiJ/osTicket-Prerequisites-and-Installation/assets/153237878/e0814bc4-def7-4639-928a-27fbf7944dfb)
- Reload IIS (Open IIS, Stop and Start the server)
- Install osTicket v1.15.8
- Extract and copy “upload” folder to c:\inetpub\wwwroot
- Within c:\inetpub\wwwroot, Rename “upload” to “osTicket”
- Reload IIS (Open IIS, Stop and Start the server)
-  Within IIS Go to sites -> Default -> osTicket -> On the right, click “Browse *:80”

![image](https://github.com/ArmandiJ/osTicket-Prerequisites-and-Installation/assets/153237878/b1be6aae-4c0b-466a-b486-d71125d3681e)
- Note that some extensions are not enabled
- Go back to IIS, sites -> Default -> osTicket -> Double-click PHP Manager -> Click “Enable or disable an extension”
- Enable: php_imap.dll
- Enable: php_intl.dll
- Enable: php_opcache.dll
- Refresh the osTicket site in your browse, observe the changes
![image](https://github.com/ArmandiJ/osTicket-Prerequisites-and-Installation/assets/153237878/dd1ce3ae-5a2f-4f48-8750-4a4c4bf57583)

- Rename: ost-config.php ->  From: C:\inetpub\wwwroot\osTicket\include\ost-sampleconfig.php ->  To: C:\inetpub\wwwroot\osTicket\include\ost-config.php
- Assign Permissions: ost-config.php
- Disable inheritance -> Remove All
- New Permissions -> Everyone -> Full Control
- Continue Setting up osTicket in the browser (click Continue)
- Name Helpdesk
- Default email (receives email from customers)
- Download and install HeidiSQL. -> Open Heidi SQL -> Create a new session, root/Password -> Connect to the session -> Create a database called “osTicket”
- Continue Setting up osticket in the browser
- MySQL Database: osTicket
- MySQL Username: root
- MySQL Password: Password You Created
- Click “Install Now!”

Congratulations, hopefully it is installed with no errors!
- Browse to your help desk login page: http://localhost/osTicket/scp/login.php
- End Users osTicket URL: http://localhost/osTicket/ 

Clean up
- Delete: C:\inetpub\wwwroot\osTicket\setup
- Set Permissions to “Read” only: C:\inetpub\wwwroot\osTicket\include\ost-config.php

