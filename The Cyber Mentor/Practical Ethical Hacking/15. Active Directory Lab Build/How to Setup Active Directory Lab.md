### Minimum Requirements
![[Min Requirements.png]]

### ISO Files Links
[Windows 10 Enterprise](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-10-enterprise)
[Windows 11 Enterprise](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-11-enterprise)
[Windows Server Essentials 2019](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2019-essentials)
[Windows Server 2022](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2022)

### Setting Up Domain Controllers
[Install Windows Server on VMware](https://academy.tcm-sec.com/courses/1152300/lectures/24769637)
[Windows Server 2022 Installation](https://www.youtube.com/watch?v=58Ul1hZRXxU)

### Setting Up User Machines
[Install Windows Enterprise on VMware](https://academy.tcm-sec.com/courses/1152300/lectures/24769673)
[Windows 10 Installation on Virtual Box](https://www.youtube.com/watch?v=JT8EXoobjSc)

##### Notes After Installation
1. Install VMware Tools
2. Rename The PC **(System Settings → About → Rename This PC)**

### Setting Up Users, Groups & Policies
[Domain Configuration](https://academy.tcm-sec.com/courses/1152300/lectures/24769638)
##### Configure Domain Controller
1. Tools → Active Directory Users & Computers
2. Create New Organizational Unit → Name it Groups<br>![[Configuration Image (1).png]]
3. Copy All Groups From Users to Groups (Leave Admin & Guest)
4. Create 2 New User<br>![[Configuration Image (2).png]]<br>![[Configuration Image (3).png]]<br>![[Configuration Image (4).png]]
5. Copy Another User Administrator<br>![[Configuration Image (5).png]]
6. Create a SQL Service Account (Don't Make It Domain Admin)<br>![[Configuration Image (6).png]]
7. Final Looks<br>![[Configuration Image (7).png]]

##### Setup a File Share
1. Server Manager → File & Storage Services → Shares
2. On Task Button Choose New Share → Quick 
3. Specify Share Name → Next → …<br>![[Configuration Image (8).png]]
4. Final Looks <br>![[Configuration Image (9).png]]

##### Creating SPN (Service Principle Name)
1. Open CMD as Administrator
2. `setspn -a <Domain-Controller-Name>/<SQL-Service-Name>.Marvel.local:60111 Marvel\SQLService`
3. `setspn -T Marvel.local -Q */*` (Check SPN Share)<br>![[Configuration Image (10).png]]

##### Disable Windows Defender
1. Open Group Policy Management Run as Administrator
2. Right Click Marvel.local as Choose Create GPO<br>![[Configuration Image (11).png]]
3. Name It Disable Windows Defender and Hit Enter
4. Right Click on Disable Windows Defender & Click Edit
5. On Computer Configuration Choose Policies → Administrative Templates → Windows Components → Windows Defender Antivirus
6. Turn off Windows Defender Antivirus → Apply → OK
7. Final Looks <br>![[Configuration Image (12).png]]

### Joining Our Machines to the Domain
[User Configuration](https://academy.tcm-sec.com/courses/1152300/lectures/24769645)
##### Create a Share Folder
1. New Folder → Share
2. Right Click → Properties → Sharing → Share → Done<br>![[Joining Everything Image (3).png]]

##### Joining to Domain Controller
1. Right Click on Network Access
2. Open Network & Internet Settings
3. Change Adapter Options
4. Right Click Ethernet 0 → Properties → IPv4
5. DNS: 192.168.57.140 `<Domain-Server-IP>`<br>![[Joining Everything Image (4).png]]
6. Access Work or School → Connect
7. Join this device → Type Domain Name (Marvel.local)
8. Join as Administrator & Type Your Password → Restart Now<br>![[Joining Everything Image (1).png]]

##### Set A Local Administrator
1. Right Click → Computer Management
2. Local Users & Groups → Groups → Administrators
3. Add → Fcastle `<Any Machine Name>`<br>![[Joining Everything Image (2).png]]