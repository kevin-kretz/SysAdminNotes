# Domains
## Domain Controllers
### DC01
1. Install Windows Server
1. Rename PC
1. Add "Active Directory Domain Services" (Server Roles)
1. Promote to Primary Domain Controller

### DC02
*Note: If setting up in VM, don't clone DC01. It will throws a set up error*
1. Install Windows Server
1. Rename PC
1. Change network adapter properties to have Default Gateway and DNS server point to DC01 IP  (Leave Backup DNS empty)
1. Install "Active Directory Domain Services"
1. Promoting to domain controller select Add to existing domain.
  a. add to existing domain
  a. copy settings from DC01

## Workstations
### Join Domain
1. Change network adapter properties to have Default Gateway and DNS server point to DC01 IP  (Leave Backup DNS empty)
1. Join domain
