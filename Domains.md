# Domains
## Domain Controllers
### Setup
#### DC01
1. Install Windows Server
1. Rename PC
1. Add "Active Directory Domain Services" (Server Roles)
1. Promote to Primary Domain Controller

### DC02
*Note: If setting up in VM, don't clone DC01. It will throws a set up error*
1. Install Windows Server
1. Rename PC
1. Change network adapter properties
   a. Set static IPv4
   b. Default Gateway and DNS server point to DC01 IP (Leave Backup DNS empty)
   c. Disable IPv6
1. Join the domain
1. Install "Active Directory Domain Services"
1. Promoting to domain controller select Add to existing domain.
  a. add to existing domain
  a. copy settings from DC01
  *This should automatically configure failover settings if done correctly.*

### Determine Primary / Failover status
1. Open `Active Directory Users and Computers`
2. Right click `[Domain Name]` > `Ooperations Masters...`

## Workstations
### Join Domain
1. Change network adapter properties to have Default Gateway and DNS server point to DC01 IP  (Leave Backup DNS empty)
1. Join domain

## Users
### Create User
1. Open `Active Directory Users and Computers`
1. Right click on `[Domain Name]` > `New` > `User`

## Groups
### Create Group
1. Open `Active Directory Users and Computers`
1. Right click on `[Domain Name]` > `New` > `Group`

## Group Policies
### Create Group Policy
1. On primary domain controller (see [Determine Primary / Failover status](###-Determine-Primary-/-Failover-status)) open `Group Policy Mangement`
1. Expand `[Forrest]` > `Domains` > `[Domain Name]` > Right click `Group Policy Objects` > `New`
1. Give GPO name (e.g. [Domain Name GPO])
1. Right click `[New GPO name]` > `Edit...`
1. Right click `[Domain Name]` > `Link an Existing GPO...`
  a. Select `[New GPO name]` > `OK`
1. Right click `[New GPO name]` > `GPO Status` > `Enabled`

### Update Group Policy Settings
1. From Client PC, open command prompt
2. Run `gpupdate /force`

### Add Share Drive
1. Update folder / drive share permissions
  a. in File Explorer, navigate to folder / drive, right click on folder / drive > `Properties`
  a. select `Properties` tab > `Advanced Sharing`
    - Check `Share this folder`
    - Give name to share drive
    - Select `Permissions`
    - Select `Add...`
      1. Enter name of group to share folder / drive with (e.g. Domain Users)
      1. select  `Check Names`
      1. select  `OK`
    - In Allow section, select `Change` permission checkbox
1. Update folder / drive NTFS permissions
  a. in File Explorer, navigate to folder / drive, right click on folder / drive > `Properties`
  a. select `Security` tab
  a. select `Edit...`
    - Select `Add...`
      1. Enter name of group to share folder / drive with (e.g. Domain Users)
      1. select  `Check Names`
      1. select  `OK`
    - Remove unnessary users (e.g. Everyone)
    - In Allow section, select `Modify` permission checkbox
1. [Create Group Policy](###-Create-Group-Policy)
1. Expand `User Configuration` > `Preferences` > `Windows Settings` > select `Drive Maps`
1. Right click in blank area > `New` > `Mapped Drive`
   a. set `Action` to `Update`
   a. set `Location:` to the file path of the shared drive / folder
   a. set name of shared drive / folder in  `Label as:`
   a. select drive letter from drop down
   a. set `Hide/Show this drive` to `Show this drive`
