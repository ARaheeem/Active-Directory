# Active-Directory Home Lab #

- **Hands-On Steps**:
    - Setting up a virtual machine (VM).
    - Configuring Server as a Domain Controller.
    - Creating Domian users.
    - Attaching Windows 11 VM to Domian.
    - Organizational Units and Gruops.
    - Gruop Policies.
    - Powershell and Automating Tasks.
    - Ressetting AD Password.

- **Software Used**:
   - Oracle Vertual Box (for VM setup).
   - Server 22 Vm.
   - Windows 11 ISO for creating a virtual environment.
   - Powershell.
 
### What is Active Directory

﻿The core of any Windows Domain is the Active Directory Domain Service (AD DS). This service acts as a catalogue that holds the information of all of the "objects" that exist on your network. Amongst the many objects supported by AD, we have users, groups, machines, printers, shares and many others. Additionally, Active directory allows you to assign what resources individuals can access , what computers they can login to and what activities they can perform. Active Directory are centralised IAM for users and resources in an organisation. Active Directory allows ease of administration by having a centralised source of truth , they inhance security and allow single point of backup and recovery.


  ### Lab Overview Step by Step Guide

  1. Download and setup Orcale Virtual Box using the follwoing link: https://knowledge.broadcom.com/external/article?articleNumber=368667
  2. Download and install Windows Server 22 vm using the follwoing link: https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022
  3. Download and install windows 11 vm using Windows 11 iso from microsoft official website.
  4. Afetr successfully downloading Windows Server 22 launch it in Oracle virual box. Create an administrative account and you will see windows server manager dashboard automatically starts up. To change your Pc using view your pc name to DC01.
5. On the server manager dashboard lick on "manage" and then "add roles and features". Then click next and select " role based or Feature based installation" and then click next to select DC01 as your server. THen click next and choose " Active Directory Domain services" which will allows us to run as a domain server.
6. Then click "add features" and make sure that the " Active Directory Domian services" option is still selected and then click next. Run with the default settings for the additional features. When the "Confirm installation selection" pop up page shows lick The "Restart option" and install.
7. In the installation pop up page select "Promote the server to a domain controller" under the Active Directory services. This will then lead to a depolyment configuration page and you must select the "add new forest" option. Then in the "Root domain name" enter Lab.local and normally here the company domain name is normally added but for our lab this should suffice. Click next and leave the "forest functional level" and "domain functional level" as default but enetr the same password you created for your admin account under "type the domain services restore mode (DSRM) password". Click next twice and allow the "NeTBIOS domian name" to automatically populate. click next until you reach the prerequisites check prompt ensuring all options are left as default. After the Prerequisite checks have been passed and confirmed click install.
8. Once the VM has restarted you should see the domain name in front of the administrator account. Allow server manager to reload and then we will be adding another role.
9. click "Manage" and Click " add roles and features". click next untill you reach the "select server role" option again. Click in the "active directory certificate service" option and then "add features".(the directory certificate service essentially allows us to use secure verion of the protocals that are needed to communicate with the server) repeat the installation process again ensuring default options are not changed. After suucessful installation click on "configure Active Directory certificate services on the destination server"
