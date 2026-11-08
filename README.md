# Active-Directory-Home-Lab
This repository showcases a working Active Directory setup within a home lab environment running proxmox. Within the environment I was able to setup:
- Domain controller, member of the server, and a Window 11 client
- Setup an Organizational Unit structure, security groups, and NTFS permissions
- Create and enforce Group Policy
- Set up DHCP on the domain controller

# Software Used
- Proxmox VE: hyporvisor
- Windows Server 2022: Domain controller and member server
- Windows 11 Pro: workstation to mimic client
- Tools within Active Directory(Active Directory Domain Services, DNS/DHCP server roles, Group Policy)

# Features
- Windows Server 2022 domain controller on domain `lab.local` with AD DS, DNS, and DHCP
- Member server and Windows 11 client joined Domain
- Delegated OU structure with role based security groups
- NTFS share permissions tied to group membership
- Group Policy Objects(desktop lockdown and automatic drive mapping)
- DHCP scope enforced within an isolated network

# Network Design
Main Lab Network(`vmbr0`)
- Linux bridge was physically connected to the home router and allowed proxmox web ui to be accessible through a management IP address

  
| VM | Role | IP |
|---|---|---|
| `SRV-DC01` | Domain Controller | 192.168.0.51 |
| `SRV-MEM01`| Member Server | 192.168.0.52 |
| `SRV-MEM02 `| Windows 11 Pro Client | 192.168.0.53 |

Isolated DHCP Network(`vmbr3`)
- A linux bridge intended for purely layer 2 switch
- DC01's second adapter (`LabNet`): 10.10.10.1/24, no gateway, no DNS server
- DHCP scope: 10.10.10.100 to 10.10.10.200

![Picture of Proxmox Network Configurations displaying vmbr0 and vmbr3](.images/proxmoxNetwork.png)


# Active Directory Design
