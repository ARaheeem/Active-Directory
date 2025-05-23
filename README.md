# Active-Directory Home Lab #

- **Hands-On Steps**:
    - Setting up a virtual machine (VM).
    - Configuring Server as a Domain Controller.
    - Creating Domian users.
    - Attaching Windows 11 VM to Domian.
    - Organizational Units and Gruops.
    - Gruop Policies.
    - Automating task using Powershell
    - Resetting AD Passwords


- **Software Used**:
   - Oracle Vertual Box (for VM setup).
   - Server 22 Vm.
   - Windows 11 ISO for creating a virtual environment.

   
 
### What is Active Directory

﻿The core of any Windows Domain is the Active Directory Domain Service (AD DS). This service acts as a catalogue that holds the information of all of the "objects" that exist on your network. Amongst the many objects supported by AD, we have users, groups, machines, printers, shares and many others. Additionally, Active directory allows you to assign what resources individuals can access , what computers they can login to and what activities they can perform. Active Directory are centralised IAM for users and resources in an organisation. Active Directory allows ease of administration by having a centralised source of truth , they inhance security and allow single point of backup and recovery.


### Lab Overview Step by Step Guide
  
**Part 1: Setting up our Server**
  1. Download and setup Orcale Virtual Box using the follwoing link: https://knowledge.broadcom.com/external/article?articleNumber=368667
  2. Download and install Windows Server 22 vm using the follwoing link: https://www.microsoft.com/en-us/evalcenter/download-windows-server-2022
  3. Download and install windows 11 vm using Windows 11 iso from microsoft official website.
  4. Afetr successfully downloading Windows Server 22 launch it in Oracle virual box. Create an administrative account and you will see windows server manager dashboard automatically starts up. To change your Pc using view your pc name to DC01.
5. On the server manager dashboard lick on "manage" and then "add roles and features". Then click next and select " role based or Feature based installation" and then click next to select DC01 as your server. THen click next and choose " Active Directory Domain services" which will allows us to run as a domain server.
6. Then click "add features" and make sure that the " Active Directory Domian services" option is still selected and then click next. Run with the default settings for the additional features. When the "Confirm installation selection" pop up page shows lick The "Restart option" and install.
7. In the installation pop up page select "Promote the server to a domain controller" under the Active Directory services. This will then lead to a depolyment configuration page and you must select the "add new forest" option. Then in the "Root domain name" enter Lab.local and normally here the company domain name is normally added but for our lab this should suffice. Click next and leave the "forest functional level" and "domain functional level" as default but enetr the same password you created for your admin account under "type the domain services restore mode (DSRM) password". Click next twice and allow the "NeTBIOS domian name" to automatically populate. click next until you reach the prerequisites check prompt ensuring all options are left as default. After the Prerequisite checks have been passed and confirmed click install.
8. Once the VM has restarted you should see the domain name in front of the administrator account. Allow server manager to reload and then we will be adding another role.
9. Click "Manage" and Click " add roles and features". click next untill you reach the "select server role" option again. Click in the "active directory certificate service" option and then "add features".(the directory certificate service essentially allows us to use secure verion of the protocals that are needed to communicate with the server) repeat the installation process again ensuring default options are not changed. After suucessful installation click on "configure Active Directory certificate services on the destination server" and click next on all default options.

**Part 2: Creating Domain Users**
1. In server Manager click on "tools" and then "Active Directory users and computers". Lick on the drop down menue of Lab local and select users file. (Note: we have yet to attach our computer therefore that folder is empty and in the domain controllers you should see the domain controler named DC01 which we created in part 1)
2. You can create additional organizational unit by right clicking on lab.local then "new" and finally "organizational unit". Name the new organizational unit "gruops" and drag all the gruops in user area into the newly created unit. add four different users by right clicking in the user unit by clicking "new" and then "users". Normally we would click the option "user must change password at next login" but for this lab its more practical to tick the option "password never expires".

**Part 3: Attaching Windows 11 VM to Domian**
1. login into the administractive account on your windows 11 vm. open up Command promt and enter in the command "ipconfig" and note down the IPv4 address , subnet mask and Default gateway.
2. Using this information we will assign static ip address for this vm machine by opening up network status and clicking "change adapter options" under the advanced network settings. Right click on Ethernet0 and selecting "properties" and double click "internet protocal version 4 (TCP/IPv4)". Select the option "use the following Ip address" and enter the Ip addresses, subnet mask and defult gateway from step 1. Additionally, enetr 127.0.0.1 in the "preferred DNS server". (To confirm this enter "ipconfig" in command prompt)
3. login on to the Window 11 vm machine and repeat the process 2 again but as "preferred DNS server" eneter the admin account ip address.
4. open up "access work or school" and select the connect option. Then select "join this device to a local Active Directory domain" and enter lab.local and enter in the admin login details.

**Part 4: Organizational units and gruop**
1. Right click on the domain then "new" and "Organizational unit" and create 3 organizational units called engineering , managment and IT. Take 2 accounts from the user folder and assign the to engineering and managment unit. Additionally, add the admininstrator account into the IT department. You could additionally create shared gruop within each department unit by selecting "new" , "gruop" and then "security". (In this lab EngineeringShared gruop was created)
2. Double click on EngineeringShare and then click on "memebers". Click "add" and enter both user in "names in object to select name".
3. Then click on "File and storage services" and then "shares". Click on task and "new shares" and click next until you see the specify share name pop up. In the Share name section enter EngineeringShare and click next until you reach the specify permission pop up. click "cutomize permission" Remove the 2 user accounts and then select "add" , "select a principle" and enter EngineeringShare. You can allocate read , write and execute permissions

**Part 5: Resetting AD passwords**
1. from the server manager dash board go to "tools" and "gruop policy management". Then right click on lab.local and select "create a GPO in this domain , and link it here" and name it "accountlockoutpolicy". then click ok and right click on the newly created GPO and select the template under computer configuration -> Polcies -> windows settings -> security settings -> account policy and finally account lockout policy.
2. To change the amount of password attempts users can perform in under account lockout threshold and for this lab we will set the 3 inavlid password attempts. A prompt will then automatically appear and ask you to assign how long the user is locked out of their accounnt but for this lab we will keep the default settings
3. To impliment this change you must right click on "accountlockputpolicy" and  click "enforced". To reset the password
 you must click on "tools" and then "active directory users and computers". to locate the users we could find them individually however a better approach is to click on the search objects option and type their name (In a larger organization entering their full name might be required). You can then assign them a new password and you should click on "user must change password at next login" but remember when creating the lab under accounts clicked the option that "password never expires"
