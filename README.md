# Ultimate-Deploy-Checklist
A document that follow up the CIA (Confidentiality, Integrality, Availability) depending on need to build network

Hardware: UPS, Load balancing, 

Multiple server -> Proxmox
Single server -> Debian

You can find specific Liinux distribution : https://distrowatch.com/

Proxmox Security:

2FA

Maximum Security Distro: QubesOS <- Same as Proxmox but without leak of security features (No Web UI, Hardware port filtering)

How to build minimal Debian based system:

Deleted useless folder
List all apt packets
Purge all packets

Debian setup:

enable unattended upgrade
enable 2FA ssh
Enable fail2ban (Limit ssh access)
Backup: BorgBackup 


Hardening:
DNS Over HTTPS/TLS
Shared storage -> ClamAV
Logwatch



minimal linux: reduce attack surface: void Linux
