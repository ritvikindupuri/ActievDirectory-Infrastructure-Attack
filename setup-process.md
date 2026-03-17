# Environment Setup Process

## Nutanix Deployment
- Installed Nutanix Community Edition (AHV) on physical servers
- Configured two clusters: G13NUTXSRV01 and G13NUTXSRV02
- Deployed Prism Central and connected both clusters

## Storage Configuration
- Created storage containers for VM deployment

## VM Template Creation
- Built Windows Server 2025 template (G13WIN2025TEMP)
- Built Windows 11 template (G13WIN11TEMP)

## Virtual Machine Deployment
- Deployed:
  - G13SRV01VM (Domain Controller)
  - G13SRV03VM (Member Server)
  - G13S1WIN11VM (Workstation)
  - G13S3WIN11VM (Workstation)

## Active Directory Configuration
- Joined VMs to domain
- Promoted servers to Domain Controllers
- Transferred FSMO roles to G13SRV01VM
- Validated replication and domain functionality

## Migration
- Migrated VMs between clusters using Prism Central
