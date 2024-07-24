![AD-002-copy](https://github.com/user-attachments/assets/ce24755c-6698-4af9-a5ae-2131f80ee991)

# Network File Shares and Permissions

In this tutorial we'll be sharing out resources over the network, as well as creating file shares to allow read, write, or deny access to individual users or groups.

# Requirements:

- Active Directory running in Azure on a virtual machine named "DC-1"
- A Client machine running in Azure on a virtual machine named "Client-1" and joined to the domaain

# Steps:

# Create some sample file shares with various permissions

- Log in to DC-1 as your domain account (mydomain.com\jane_admin)
![Screenshot 2024-07-07 184904](https://github.com/user-attachments/assets/99a87c4f-5ebd-4079-b381-e16d9a6a9fd2)

- Log in to Client-1 as a normal user (mydomain.com\<randomuser>)
![Screenshot 2024-07-14 185208](https://github.com/user-attachments/assets/4f1cbad4-afba-4ea9-982f-a2f5001e231b)

- On DC-1, on the C:\drive, create 4 folders named "read-access", "write-access", "no-access", "acconting"
![Screenshot 2024-07-14 181855](https://github.com/user-attachments/assets/50c358fc-85da-425a-866b-045dfa4e8e68)

- Right-click and select new folder
![Screenshot 2024-07-14 182315](https://github.com/user-attachments/assets/8a8cff5d-67ce-4570-ab1f-b28fe8a4c29a)
![Screenshot 2024-07-14 182457](https://github.com/user-attachments/assets/7920232b-18ea-49f2-8b1d-5b2a9fd256bd)

- Set the following permissions (share the folder) for the "Domain Users" group on DC-1. Right-click on the selected folder
![Screenshot 2024-07-14 182545](https://github.com/user-attachments/assets/ba7f4ca5-c3c0-40c2-bc54-b83529b2b680)

- On the "read-access" Go to properties > sharing > select share
![Screenshot 2024-07-14 182610](https://github.com/user-attachments/assets/c38b927d-4bd0-42cd-921b-26033ccc57de)

- Type "Domain Users" and add them
![Screenshot 2024-07-14 182653](https://github.com/user-attachments/assets/74d043aa-c228-4407-9247-3d131b8d2ec0)
![Screenshot 2024-07-14 182659](https://github.com/user-attachments/assets/46c01618-c167-4e98-9e18-ceca819c13e0)

- Set Read only for the Permission Level and Click share
![Screenshot 2024-07-14 182659](https://github.com/user-attachments/assets/75244156-21ad-4bec-a79a-afbd4ed7c314)
![Screenshot 2024-07-14 182733](https://github.com/user-attachments/assets/08b79b66-5364-4aca-88e0-fdf3ce64b2fc)

- On the "write-access" Go to properties > sharing > select share. Share folder to the Domain Users and set Permission Level to Read/Write and click share.
![Screenshot 2024-07-14 184009](https://github.com/user-attachments/assets/21947505-a5b5-4251-aab9-9459604f47e8)

- Share the "no-access" folder to Domain Admin. This will deny access to those who are not an admin. The admin will be able to read/write and normal users will not have access to the folder because only admin will have access to this folder.
![Screenshot 2024-07-14 183003](https://github.com/user-attachments/assets/ffac76fc-1d15-491b-84a8-8e0f8fec5b1a)
![Screenshot 2024-07-14 183012](https://github.com/user-attachments/assets/fbe00bf5-93e3-42ca-837c-fa70f7b99ff5)

# Attempt to access file shares as a normal user

- Go to Client-1 and navigate to the shared folders. Click start > Run > \\\dc-1
![Screenshot 2024-07-14 183527](https://github.com/user-attachments/assets/d23ba0bc-254a-49f0-8a42-d656276ed2ae)
![Screenshot 2024-07-14 183537](https://github.com/user-attachments/assets/ff86c9d5-4d04-4415-aaba-4b2064bac073)

- As you can see here the normal user cannot open the "no-access" folder because it doesn't have permissions to do so.
![Screenshot 2024-07-14 184049](https://github.com/user-attachments/assets/5a6128f6-b3de-4d86-812b-3bbc17f2bd2d)

- The normal can open the "read-access" folder because it does have permissions to do so. But lets say we want to modify the existing file, it will not allow us because the permission level is set to Read only.
![Screenshot 2024-07-14 183726](https://github.com/user-attachments/assets/83e390bf-61b5-4562-8ed9-d9560df9ec94)
![Screenshot 2024-07-14 183917](https://github.com/user-attachments/assets/6f5c9966-3bce-4348-a769-04cba40d4db8)

- The normal user can read and write for the "write-access" folder. We can create a file because we have the permissions to do so.
![Screenshot 2024-07-14 184035](https://github.com/user-attachments/assets/c717ddaf-92ab-4b7a-bc1e-4a48bab73600)

# Create an "ACCOUNTANTS" Security Groups, assign permission and test access

- Go to DC-1 in Active Directory. Go to your domain name and create new organizational unit named "_SECURITY GROUPS"
![Screenshot 2024-07-14 184513](https://github.com/user-attachments/assets/21df98a5-985b-4fe9-b58c-74dfb620d709)
![Screenshot 2024-07-14 184528](https://github.com/user-attachments/assets/06626feb-8040-4166-a0f7-688e91d42c65)

- Select and right click "_SECURITY GROUPS" and create new group named "Accountants"
![Screenshot 2024-07-14 184536](https://github.com/user-attachments/assets/3bf1736d-bff2-4042-8b84-c0bb19b4f8b1)
![Screenshot 2024-07-14 184553](https://github.com/user-attachments/assets/8d828a11-65d0-493c-a346-e46223627f00)

- Make sure Security is the Group Type. We are not going to add anyone to this group yet, we are just going to assign permissions for now.
![Screenshot 2024-07-14 184621](https://github.com/user-attachments/assets/5577c4bc-c7be-476f-beb9-f086f6c32dde)

- Go to the "Accounting" folder > Properties
![Screenshot 2024-07-14 184718](https://github.com/user-attachments/assets/9ce46380-0ab1-470b-9eec-d3612d6a67d7)

- Share folder to the Accountants Group
![Screenshot 2024-07-14 184755](https://github.com/user-attachments/assets/24cee327-30f6-4c4e-ba20-8577dbc50bfe)
![Screenshot 2024-07-14 184804](https://github.com/user-attachments/assets/ca26a22e-3d2e-45ac-b7e9-2f7e7c2603d6)

- Attempt to open the "Accountant" folder as a normal user and observe. The normal user does not have access becasue only the Security Group "Accountants" have access only.
![Screenshot 2024-07-14 184843](https://github.com/user-attachments/assets/76cb6128-134f-4fc3-90ec-c83f68b2dcaf)

- On DC-1, make your normal user a member of the "ACCOUNTANTS" Security Groups. Type the name of your normal user and add them.
![Screenshot 2024-07-14 185043](https://github.com/user-attachments/assets/9980d4ba-a1cf-4ffb-a00f-55d2c354dd18)
- Apply settings
![Screenshot 2024-07-14 185052](https://github.com/user-attachments/assets/a784769c-efeb-477c-92aa-5db424b5b7d6)

- Log out and log back in to Client-1 as your normal user. Everytime there is a change in permissions or change in groups, you will have to log out and log back in to get your permissions assign to you.

![Screenshot 2024-07-14 185208](https://github.com/user-attachments/assets/8e74a790-a227-4ae0-a80c-1a2f7031f9bf)

- Now attempt to access the "Accountants" folder with your new assign permissions
![Screenshot 2024-07-14 185312](https://github.com/user-attachments/assets/7a7aacae-1767-4de2-a762-9e3106c82202)
![Screenshot 2024-07-14 185349](https://github.com/user-attachments/assets/3be86cb8-6c4a-4b7f-8157-c6cf4c193b08)

This brings the conclusion for this tutorial! Thank you for watching :)

































