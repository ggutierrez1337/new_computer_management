# Pre-Staging Computers and Redirecting New Computers to a dedicated OU

## Description
This project outlines the process of managing computer accounts within an Active Directory (AD) environment, focusing on the use of pre-staged computer accounts, adding computers to specific groups for enhanced security, and creating custom Organizational Units (OUs). These techniques improve the structure, management, and security of computer objects within an AD domain.

## Tools and Utilities

- **Windows Server (with Active Directory Domain Services)**: Primary environment for managing computer accounts and configuring policies.
- **Active Directory Users and Computers (ADUC)**: Used for creating, managing, and organizing computer accounts.
- **Command Prompt (cmd)**: Executed domain redirection commands.
- **PowerShell**: Relevant for scripting and automating AD tasks (not directly covered but useful for advanced implementations).

## Environments

### Server Environment
- **Operating System**: Windows Server configured with Active Directory Domain Services (AD DS).
- **AD Configuration**: Set up with pre-staged computer accounts and custom OUs for structured management.


## Program Walkthrough

### Pre-staging a Computer
1. Accessed **Active Directory Users and Computers (ADUC)** and right-clicked the **Computers** container.
2. Selected **New** → **Computer** and named the new computer account.
3. Documented that pre-staged computers automatically attach themselves to their respective objects when added to the domain, enhancing administrative readiness.

### Adding a Computer to a Group
1. Right-clicked an existing computer in **ADUC** and reviewed available options.
2. Assigned the computer to a specific security group to restrict access and add an extra layer of security to domain resources.
3. Highlighted that assigning computers to groups is essential for fine-tuning resource access based on computer-specific policies.

### Creating a New Organizational Unit (OU)
1. Created a new **OU** under the domain to house all new computers, preventing them from defaulting to the **Computers** container.
2. Implemented security measures to detect unauthorized additions (e.g., Shadow IT).
3. Used the `REDIRCMP` command to redirect new computer accounts to the newly created OU:
   ```bash
   REDIRCMP “OU=New Computers, DC=YourDomain, DC=Local”



## Managing New Computer Accounts

## **Scenario**

Pre-Stage a computer in the Computers container ensuring that if a PC is added to the domain, there is a one already staged and will be attached to pre-staged computer in the **Computers** container. Create an OU for New Computers and redirect new computers added to the the domain to be attached to that folder. Every time a new computer is joined to the domain, they should be added to the **New Computers** OU and **not Computers** OU

### Pre-staging a Computer

1. In **Active Directory Users and Computers** tool, right click the **Computers** container and select **New → Computer**

![image](https://github.com/user-attachments/assets/6c1bb54e-75bb-4221-ba5a-658773b96f22)

2. Name the computer that will be created
    - Once created, if one were to add a new computer to the domain, it will automatically attach itself to the new computer created 

![image 1](https://github.com/user-attachments/assets/6b8f0ef1-f811-46fc-b2e1-e1031cc7d697)

![image 2](https://github.com/user-attachments/assets/c6eef7bf-4cf3-4695-a487-c0e01f1d425f)

### Adding a Computer to a Group

Users can be assigned to a specific group in the case where only they should be accessing specific resources, but it can be taken a step further and add their specific computer as well to only access those resources by **assigning the computer to a group**

Can mainly be used as an **additional layer of security**

1. Right click the computer and view the options available with the computer 

![image 3](https://github.com/user-attachments/assets/6ec104e2-0c03-48eb-96f0-d170f5083e96)

### Creating a New Organizational Unit for New Computers

Can be done in the cases where admins want to have all new computers to the Domain Controller sent to a different container rather than the **Computers** container

**Can help with security in catching bad actors assigning new computers to the DC and also prevent Shadow IT**

2. In **Active Directory Users and Computers** tool, right-click the domain and select **New Organizational Unit,** and name the OU
    - A new OU Container will be present in the domain

![image 4](https://github.com/user-attachments/assets/0ac635dd-31cf-4c12-9d2a-2c2bbbd62fcd)

![image 5](https://github.com/user-attachments/assets/55b68eab-fdd6-4b94-b004-dcd27140634b)

![image 6](https://github.com/user-attachments/assets/51b47841-1b60-46fb-85a2-189553edd1b9)

3. In cmd, type **REDIRCMP “OU=Organizational Unit, DC=Domain Controller, DC=Local”**
    - e.g. - REDIRCMP “OU=New Computers, DC=WINSERV, DC=LOCAL”
    - Command to redirect computer- REDIRCMP
    - OU - Organizational Unit
    - DC - Domain Component (Each part of the domain name is separate component (WINSERV.LOCAL))

![image 7](https://github.com/user-attachments/assets/b7428e84-7798-4084-96bb-7818ca559219)

# Summary 
This project enhances the management of computer objects in an Active Directory domain by employing strategic placements and group assignments. It provides a structured approach for handling computer accounts, improving security, and ensuring better administrative oversight. By pre-staging computers and redirecting them to specific OUs, this project promotes a streamlined, controlled environment, reducing risks associated with unauthorized domain access.
