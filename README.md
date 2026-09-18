# Active Directory Home Lab (Phase 1: Domain Infrastructure)

A self-built Windows Server 2022 domain environment on Oracle VirtualBox, covering
Active Directory Domain Services, DNS, DHCP, NAT/routing, and PowerShell-based
user provisioning. This is Phase 1 of a larger lab — Phase 2 forwards logs from
this domain to a Wazuh SIEM for detection and alerting work (see "What's Next").

## Why this project

Most entry-level cybersecurity roles assume familiarity with how a Windows
domain actually works — how authentication, name resolution, and address
assignment fit together, and how admins manage all of it at scale. Rather than
just read about it, I built the environment from scratch to develop that
intuition, including troubleshooting it when something didn't work the first
time.

## Architecture

- **Domain Controller** (Windows Server 2022): AD DS, DNS, DHCP, IIS, Remote
  Access (RRAS/NAT) roles, running as `mydomain.com`
- **Client-1** (Windows 11 Pro): domain-joined workstation on the internal
  network, obtaining its IP via DHCP
- Two-NIC design on the DC: one NAT-connected for outbound internet, one on an
  internal-only network for the client — the DC does double duty as gateway,
  DNS server, and domain controller for that internal segment

## What I built

1. **Installed and configured server roles** — AD DS, DNS, DHCP, IIS, and
   Remote Access on a single Windows Server 2022 instance, promoted to a new
   forest/domain (`mydomain.com`).
2. **Created an OU structure** — separate `_ADMINS` and `_USERS` organizational
   units, with a dedicated domain-admin account (rather than using the
   built-in Administrator) added to Domain Admins.
3. **Configured DHCP** — a scope (`172.16.0.100`–`172.16.0.200`) with router
   and DNS server options pointed at the domain controller, so clients get a
   full working configuration automatically.
4. **Automated user creation with PowerShell** — a script that reads a name
   list, generates usernames (first-initial + last name), and bulk-creates AD
   user accounts under the `_USERS` OU with `New-ADUser`, rather than creating
   accounts one at a time through the GUI.
5. **Joined a client to the domain** — a Windows 11 client received its IP,
   subnet, gateway, and DNS server from DHCP, joined `mydomain.com`, and
   authenticated with a domain account.
6. **Verified end-to-end** — confirmed DHCP lease assignment, domain
   authentication (`whoami`, `echo %logonserver%`), and correct network
   configuration (`ipconfig /all`) from the client side.

## Screenshots

| # | File | What it shows |
|---|------|----------------|
| 01 | `01-server-roles.png` | Server Manager dashboard — AD DS, DNS, File and Storage Services, IIS, and Remote Access all installed |
| 02 | `02-domain-created.png` | Active Directory Users and Computers showing the newly created `mydomain.com` forest |
| 03 | `03-admin-ou-user.png` | `_ADMINS` OU with the dedicated domain-admin account |
| 04 | `04-dhcp-scope.png` | Active DHCP scope (`172.16.0.0`, range `.100`–`.200`) |
| 05 | `05-powershell-user-creation.png` | PowerShell script bulk-creating AD users, with live console output |
| 06 | `06-active-directory-users.png` | `_USERS` OU populated by the script |
| 07 | `07-client-dhcp-ip.png` | Client `ipconfig` output confirming DHCP-assigned addressing |
| 08 | `08-domain-joined-client.png` | Client system info confirming domain join (`CLIENT1.mydomain.com`) |
| 09 | `09-final-domain-verification.png` | Client-side verification: `whoami`, `ipconfig /all`, `hostname`, and `echo %logonserver%` all confirming successful domain membership and authentication |

## Skills demonstrated

- Windows Server role installation and configuration (AD DS, DNS, DHCP, RRAS/NAT)
- Active Directory forest/domain creation and OU design
- DHCP scope design (addressing, lease options, gateway/DNS options)
- PowerShell scripting for bulk account provisioning (`New-ADUser`, string
  manipulation, loops)
- Client domain-join workflow and authentication verification
- Basic network troubleshooting in a virtualized routed environment

## What's next (Phase 2)

This domain controller and client are the foundation for a larger lab that
also includes a Wazuh SIEM (Ubuntu) and a NAS acting as a syslog target. The
next phase forwards Windows Security event logs from this domain to Wazuh,
enables relevant audit policies, and documents at least one detection mapped
to MITRE ATT&CK — the part of this project most directly relevant to a SOC
analyst role.

## Credit

Built by following a public YouTube walkthrough on setting up a Windows
Server Active Directory lab in VirtualBox, then adapted and documented in my
own words based on what I actually configured.
