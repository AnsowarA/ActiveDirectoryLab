# Active Directory Home Lab

## Overview

This project documents the deployment and configuration of a Windows Active Directory environment in a virtualized home lab.

The purpose of this lab was to gain hands-on experience with:

- Windows Server administration
- Active Directory Domain Services
- DNS
- DHCP
- Organizational Units
- Domain administrator accounts
- PowerShell automation
- User provisioning
- Windows client domain joining
- Domain authentication
- Windows networking
- Troubleshooting client connectivity

The environment was built using Oracle VirtualBox with a Windows Server virtual machine acting as the domain controller and a Windows 11 Pro client machine joined to the Active Directory domain.

---

## Lab Objectives

The main objectives of this project were to:

- Deploy a Windows Server virtual machine
- Configure the server as a domain controller
- Create a new Active Directory forest and domain
- Configure DNS services
- Configure DHCP for client addressing
- Create Organizational Units
- Create an administrative account
- Use PowerShell to automate user creation
- Join a Windows 11 workstation to the domain
- Log in using domain credentials
- Verify client connectivity and domain authentication

---

## Technologies Used

- Oracle VirtualBox
- Windows Server
- Windows 11 Pro
- Active Directory Domain Services
- DNS
- DHCP
- PowerShell
- Windows Server Manager
- Active Directory Users and Computers
- Command Prompt

---

# Lab Environment

The lab consisted of two primary virtual machines.

## Domain Controller

The Windows Server virtual machine was configured as the domain controller.

The domain controller was responsible for:

- Active Directory Domain Services
- DNS
- DHCP
- User account management
- Organizational Unit management
- Domain authentication
- Client IP addressing

The domain used in the lab was:

```text
mydomain.com
