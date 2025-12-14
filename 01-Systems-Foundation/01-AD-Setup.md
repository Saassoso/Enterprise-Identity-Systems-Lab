## PRE-REQUISITES (Before Installing AD)
### Installing Windows Server 2022 
![[Pasted image 20251214122740.png]]
### Set a Static IP 
Open PowerShell and type : `ipconfig /all`
![[Pasted image 20251214123000.png]]
- Note your **IPv4 Address**, **Subnet Mask**, and **Default Gateway**.
![[Pasted image 20251214123256.png]]
- Note your **IPv4 Address**, **Subnet Mask**, and **Default Gateway**.
- Go to **Control Panel** > **Network and Internet** > **Network Connections**.
- Right-click your adapter > **Properties** > **IPv4** > **Properties**.

Use the IP address of the automatically allocated , and click Ok :
- **IP Address:** `192.168.88.138`
- **Subnet Mask:**  `255.255.255.0`.
- **Gateway:** `192.168.88.2`
- **Preferred DNS Server:** **127.0.0.1** (The DC must point to itself for DNS).
- **Alternate DNS:** `8.8.8.8` (Google, for internet access).

![[Pasted image 20251214123337.png]]
### Rename the Server
- We change the Computer Name to `DC01`
![[Pasted image 20251214124133.png]]
## Install & PROMOTE
### Install the AD DS Role
- Click **Manage** (top right) > **Add Roles and Features**.
![[Pasted image 20251214124339.png]]

![[Pasted image 20251214124428.png]]

![[Pasted image 20251214124446.png]]
- On Server Roles : Check **Active Directory Domain Services**. 
![[Pasted image 20251214124606.png]]
- Click Add Features.
![[Pasted image 20251214124512.png]]
- Click Next all the way to Confirmation.
![[Pasted image 20251214124711.png]]
- Install it an wait for the installation to finish.
![[Pasted image 20251214124743.png]]
### Promote to Domain Controller
To promote the server to domain controller there is 2 option :
- Click it here after installation :
![[Pasted image 20251214124917.png]]
- On the yellow triangle, at the top right flag icon. Click it
![[Pasted image 20251214125005.png]]
- Select: **Add a new forest** , and write the root domain name `lab.local`
![[Pasted image 20251214125214.png]]
- Then on Domain Controller Options : 
	- Leave Forest/Domain functional level at Windows Server 2016, to ensure compatibility.
	- Type a DSRM Password, that help boot into **Safe Mode**.
![[Pasted image 20251214125611.png]]
- Ignore the yellow warning
![[Pasted image 20251214125642.png]]
- **Additional Options:** Verify NetBIOS name is `LAB`
![[Pasted image 20251214125719.png]]
- **Paths:** Leave defaults.
![[Pasted image 20251214125816.png]]
- **Prerequisites Check:** Wait for the green checkmark.
We got 2 problem , 1 which is critical :
- The Administrator password is blank 
![[Pasted image 20251214125938.png]]
- So we set a password 
![[Pasted image 20251214130202.png]]
- The click **Rerun Prerequisites Check**, and we get the green checkmark.
![[Pasted image 20251214130346.png]]
- Click **Install** to begin installation.
![[Pasted image 20251214130432.png]]
- The server will reboot automatically. 
## VERIFICATION
### Login & Verify
- When it comes back up, the login screen should say: `LAB\Administrator`.
![[Pasted image 20251214131943.png]]
- Login.
- Open **Server Manager** > **Tools** (top right) and verify you see **Active Directory Users and Computers**.
	- Open it. You should see your domain `lab.local`.
![[Pasted image 20251214131530.png]]
## Disclaimer 
For the 2 warning we got at the installation :
![[Pasted image 20251214130650.png]]
- **The Cryptography Warning:** Means your server is too modern for computers from 1996. **Ignore it.**
- **The DNS Warning:** Means "I cannot find a parent company above you." This is correct because you _are_ the parent company. **Ignore it.**