# osTicket: Prerequisites and Installation
<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>
In this lab, I set up osTicket from scratch using the needed files. Before installing the ticketing system, I completed a few setup steps. The lab was done on a Windows 10 Pro virtual machine in Azure. This lab uses a Windows 10 Pro virtual machine created on Azure. All the necessary installation files used in the process can be found <a href="https://drive.google.com/drive/u/0/folders/1APMfNyfNzcxZC6EzdaNfdZsUwxWYChf6">Here!</a>


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Internet Information Services (IIS)
- MySQL

<h2>Operating Systems Used </h2>

- Windows 10</b> (21H2)
  


<h2>Installation Steps</h2>
<img width="1128" alt="Screenshot 2024-11-21 at 2 11 51 PM" src="https://github.com/user-attachments/assets/3863115b-b34a-41cd-a4e5-a21c63071392">

<img width="1122" alt="Screenshot 2024-11-21 at 2 12 41 PM" src="https://github.com/user-attachments/assets/20595003-8d1b-4ecd-95ac-309fa124e5ad">
<p>
</p>
<p>
Before installing any files, it is necessary to enable Internet Information Services (IIS), as osTicket requires IIS to function locally. To enable IIS, open the Control Panel and navigate to Programs, then select "Turn Windows Features On or Off." In the features menu, expand Internet Information Services, then expand Web Management Tools, and enable IIS Management Console. Next, expand World Wide Web Services, followed by Application Development Features, and ensure CGI is enabled. Finally, click OK to confirm and apply the changes.
<p>      
</p>
<p>


  
  <img width="1115" alt="Screenshot 2024-11-21 at 2 21 43 PM" src="https://github.com/user-attachments/assets/900ca078-6609-4a6c-8c6e-e4d68c6048a4">
  <p>
  </p>
  <p>
After enabling IIS, download and install PHP Manager for IIS (PHPManagerforIIS_V1.5.0.msi) from the installation files folder. Once PHP Manager is installed, proceed to download and install the Rewrite Module (rewrite_amd64_en-US.msi). PHP is a backend web server language, and osTicket operates using PHP.
<p> 
</p>
<p>
  <p>
    <img width="953" alt="Screenshot 2024-11-21 at 2 29 01 PM" src="https://github.com/user-attachments/assets/6cce4073-7a14-43e1-9e20-245205f798f6">
    
After installing the Rewrite Module, create a new folder/directory called C:\PHP on the Windows (C:) drive. This new folder will be used to unzip the contents from the PHP 7.3.8 (php-7.3.8-nts-Win32-VC15-x86.zip) zip folder downloaded from the installation files. Extract all contents from the zip folder into the C:\PHP folder.
<p>
</p>
<p>
<img width="476" alt="Screenshot 2024-11-21 at 2 31 02 PM" src="https://github.com/user-attachments/assets/1f0b3949-0272-4925-94df-88f8b1e02625">

Next install VC_redist.x86.exe from installation file.
<p>
</p>
<p>
<img width="497" alt="Screenshot 2024-11-21 at 2 35 36 PM" src="https://github.com/user-attachments/assets/fd7f90bd-15e2-451c-ac14-8f092de592f6">

Next, download and install MySQL 5.5.62 (mysql-5.5.62-win32.msi) from the installation files. During the MySQL setup wizard, click "I agree," choose a Typical installation, and proceed with Install. After the installation is complete, launch the Configuration Wizard. Select Standard Configuration, check Install as Windows Service, and ensure Launch the MySQL Server automatically is selected. For the credentials, use root as the username and Password1 as the password. In a real-world scenario, more secure credentials should be used, but for the purposes of this lab, the default root and Password1 credentials will suffice. 

MySQL is a database osTicket is going to use to store all our data like user accounts, ticketing info etc.
<p>
</p>
<p>
<img width="1085" alt="opening IIS as an admin" src="https://github.com/user-attachments/assets/fc6ca27a-a7f7-46e6-a3ed-5ff3b3751624">
<img width="1085" alt="Screenshot 2024-11-21 at 2 54 46 PM" src="https://github.com/user-attachments/assets/6e6afcba-3d51-4f2a-a0c4-9b02408ae8eb">

Next, open IIS as an administrator and select PHP Manager. To register PHP within IIS, open the PHP Manager and choose Register New PHP Version. Click Browse and select the php-cgi.exe file located in the PHP folder created earlier in the lab. Finally, reload the IIS server from within the management console.
<p>
</p>
<p>
<img width="664" alt="copying the upload folder" src="https://github.com/user-attachments/assets/adc3b438-aa24-4b47-9f87-2685fd9e5862">

From installation file download osTicket v1.15.8. and copy the “upload” folder to c:\inetpub\wwwroot. And rename it ti ‘osTicket’.
<p>
</p>
<p>
<img width="1470" alt="browsing the OS ticket" src="https://github.com/user-attachments/assets/e2727684-ccc2-477c-afbf-4f3db007b3f2">
<img width="876" alt="enabling some extensions" src="https://github.com/user-attachments/assets/d7184ec3-d284-40d3-a0c5-0858119768ef">

  
In the IIS console, navigate to Sites -> Default -> osTicket. Click on *Browse :80, and the osTicket installation page will appear. Some required extensions are not enabled by default, so they need to be activated in the IIS console before installing osTicket. To enable these extensions, click on PHP Manager while in the osTicket menu in IIS. Then, select Enable or Disable an Extension and enable the following extensions: php_imap.dll, php_intl.dll, and php_opcache.dll.
<p>
</p>
<p>
<img width="765" alt="changing permission " src="https://github.com/user-attachments/assets/6ceb81b0-389a-447b-bf39-95cfb1033769">

One file needs to be renamed ost-sampleconfig.php to os-comnfig.php. This file will have it’s permission changed. Go to it’s properties and change the permissions : Disable inheritance to > Remove All and New Permissions -> Everyone -> All
<p>
</p>
<p>
<img width="599" alt="Screenshot 2024-11-21 at 3 33 06 PM" src="https://github.com/user-attachments/assets/ce432b57-3307-4a6b-8043-c3aed0550f33">
<img width="1372" alt="Screenshot 2024-11-21 at 3 36 26 PM" src="https://github.com/user-attachments/assets/edfb8967-1540-4e4f-8a61-727530079b4a">

After completing the previous steps, open the osTicket installation page in your browser and fill in the required details, such as name, password, and other information. Before clicking Next, install HeidiSQL from the osTicket installation files. HeidiSQL will allow you to connect to the database. Create a new session in HeidiSQL and enter the password you set during the MySQL installation. In the new session, right-click on Unnamed and create a new database named osTicket.
<p>
</p>
<p><img width="783" alt="Screenshot 2024-11-21 at 3 37 45 PM" src="https://github.com/user-attachments/assets/9046faed-e991-4f08-8852-9e8ced4d9166">
<img width="781" alt="Screenshot 2024-11-21 at 3 42 14 PM" src="https://github.com/user-attachments/assets/2e30a289-c6f1-4847-86fa-092b953aa7ac">

In the osTicket browser window, enter the required details to set up osTicket. For the MySQL database, use the same credentials as those set in MySQL and HeidiSQL. The username should be root, and the password will also be root. Once these steps are completed, osTicket should be installed and ready to use.

osTicket Installed. 

osTicket is now successfully installed and ready to use. Through this lab, I explored how ticketing systems function and how to manage and resolve tickets effectively. In IT Support, working collaboratively with a team to address IT-related issues often involves using a ticketing system. This lab served as a hands-on experience to set up a ticketing system from scratch, providing a foundation for the work I aim to undertake in the future.

































