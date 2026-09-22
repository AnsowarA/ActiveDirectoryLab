# Active Directory Home Lab

## Project Overview

This project documents the step-by-step process I used to build a Windows Active Directory lab in Oracle VirtualBox.

---

# Step 1 - Verify Windows Server Roles

I configured the Windows Server environment with the required services.

### Verification

![Windows Server Roles](screenshots/04-server-roles.png)

---

# Step 2 - Create the Active Directory Domain

I promoted the Windows Server machine to a domain controller and created the domain:

`mydomain.com`

### Verification

![Active Directory Domain](screenshots/05-domain-created.png)

After the server was promoted to a domain controller, I opened Active Directory Users and Computers to verify that the domain was created successfully.

Verification

This screenshot confirms that:

The Active Directory domain was created
The server was functioning as a domain controller
mydomain.com was available in Active Directory Users and Computers
Step 3 - Create an Administrative Organizational Unit

I created a dedicated Organizational Unit for administrative accounts.

The OU was named:

_ADMINS

I then created an administrative account inside the _ADMINS Organizational Unit.

Verification

This screenshot confirms that:

The _ADMINS OU was created
An administrative user account was added
Active Directory objects were being organized into separate containers
Step 4 - Configure DHCP

I configured DHCP on the domain controller so client computers could automatically receive network settings.

The DHCP scope was configured for the following IP address range:

172.16.0.100 - 172.16.0.200

The scope was activated after configuration.

Verification

This screenshot confirms that:

The DHCP service was configured
The IPv4 scope was active
The server was ready to assign IP addresses to client machines
Step 5 - Automate User Creation with PowerShell

Instead of creating users manually one at a time, I used PowerShell to automate the process.

The script created Active Directory user accounts and placed them inside a dedicated Users Organizational Unit.

The script used Active Directory PowerShell commands such as:

New-ADOrganizationalUnit
New-ADUser
Verification

This screenshot shows PowerShell actively creating Active Directory user accounts.

This demonstrates how scripting can be used to automate repetitive administrative tasks.

Step 6 - Verify the Users Were Created

After the PowerShell script completed, I opened Active Directory Users and Computers to verify that the accounts were created successfully.

A dedicated Organizational Unit named:

_USERS

contained the newly created user accounts.

Verification

This screenshot confirms that:

The PowerShell script successfully created users
The accounts appeared inside Active Directory
The users were placed in the correct Organizational Unit
Step 7 - Verify the Client Received Network Configuration

After creating the Windows client machine, I checked its network configuration.

I ran:

ipconfig

The client received:

IPv4 Address: 172.16.0.100
Subnet Mask: 255.255.255.0
Default Gateway: 172.16.0.1
DNS Suffix: mydomain.com
Verification

This screenshot confirms that:

DHCP was working
The client received an IP address automatically
The client was on the correct internal network
The client received the domain DNS suffix
Step 8 - Join the Windows 11 Client to the Domain

I joined the Windows 11 Pro client machine to the Active Directory domain.

The full device name showed:

CLIENT1.mydomain.com
Verification

This screenshot confirms that:

The Windows 11 client successfully joined the domain
The client could locate the domain through DNS
The workstation became part of the Active Directory environment
Step 9 - Verify Domain Authentication and Connectivity

After joining the client to the domain, I logged in with a domain account and ran several commands to verify that the environment was working properly.

Verify the Domain User

I ran:

whoami

The output showed:

mydomain\abilderback

This confirmed that the user was authenticated through Active Directory.

Verify Network Configuration

I ran:

ipconfig /all

Important values included:

DHCP Enabled: Yes
DHCP Server: 172.16.0.1
DNS Server: 172.16.0.1
DNS Suffix: mydomain.com
Verify the Hostname

I ran:

hostname

The output showed:

CLIENT1
Verify the Logon Server

I also ran:

echo %logonserver%

This confirmed that the client was authenticating through the domain controller.

Verification

This final screenshot confirms that:

The client was joined to the domain
A domain account could log in successfully
DHCP was working
DNS was working
The hostname was correct
The client was communicating with the domain controller
Active Directory authentication was functioning
Final Lab Result

At the end of the lab, the environment included:

Windows Server Domain Controller
|
|-- Active Directory Domain Services
|-- DNS
|-- DHCP
|-- Administrative OU
|-- Users OU
|-- PowerShell User Automation
|
Windows 11 Client
|
|-- Joined to mydomain.com
|-- Received DHCP Address
|-- Used Domain DNS
|-- Logged in with Domain Account
|-- Verified Domain Controller Communication
Skills Practiced

This lab gave me hands-on experience with:

Windows Server administration
Active Directory Domain Services
Domain controller deployment
Active Directory domain creation
Organizational Units
Administrative account management
DHCP
DNS
PowerShell automation
Automated user provisioning
Windows 11 domain joining
Domain authentication
TCP/IP networking
Client verification
Troubleshooting
Virtual machine administration
What I Learned

This lab helped me understand how a Windows domain environment works from both the server and client side.

I gained hands-on experience with:

Creating an Active Directory domain
Managing users and Organizational Units
Automating user creation with PowerShell
Configuring DHCP
Joining a Windows workstation to a domain
Logging in with domain credentials
Verifying authentication
Verifying client network connectivity
Troubleshooting Windows domain communication
Future Improvements

I plan to expand this Active Directory lab with additional administration and security projects.

Possible future improvements include:

Group Policy Objects
Password policies
Account lockout policies
Security groups
Shared folders
NTFS permissions
Windows Event Logging
Sysmon
Wazuh integration
Splunk integration
Active Directory security testing
Windows Server hardening
Centralized logging
PowerShell logging
Screenshot Summary
Screenshot	Description
04-server-roles.png	Windows Server roles installed
05-domain-created.png	Active Directory domain created
06-admin-ou-user.png	Administrative OU and account
08-dhcp-scope.png	Active DHCP scope
09-powershell-user-creation.png	PowerShell automated user creation
10-active-directory-users.png	Created Active Directory users
11-client-dhcp-ip.png	Client DHCP configuration
12-domain-joined-client.png	Windows client joined to the domain
14-final-domain-verification.png	Final authentication and network verification
Acknowledgment

This lab was completed as a hands-on learning project while following an Active Directory home lab tutorial.

The environment was personally configured, tested, verified, and documented as part of my Windows administration and cybersecurity practice.

