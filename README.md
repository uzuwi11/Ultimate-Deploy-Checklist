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



QubesOS (Dom0)
│
├── VM-FW-Core (pfSense master)
│   ├── Politique générale : Default DROP, routage inter-zones strict
│   └── NAT, VLANs, logs centralisés
│
├── ┬── Workstation VMs
│   │   ├── fw-work
│   │   │   ├── OUTPUT only (conntrack NEW), INPUT DROP
│   │   │   └── NIDS/NIPS activé (ex: Suricata + Fail2ban ou Snort)
│   │   └── vm-work (Web, Mail, DevTools)
│   │
├── ┬── Admin VMs
│   │   ├── fw-admin
│   │   │   ├── Entrées limitées (SSH, Web admin), monitoring actif
│   │   │   └── NIDS/NIPS activé
│   │   └── vm-admin (bastion, ansible, supervision)
│   │
├── ┬── Internal Servers
│   │   ├── fw-internal
│   │   │   └── INPUT contrôlé, OUTPUT via proxy si besoin
│   │   └── vm-db, vm-api, vm-auth
│   │
├── ┬── Public DMZ
│   │   ├── fw-dmz
│   │   │   └── NAT/Port Fwd précis, journaux renforcés
│   │   └── vm-web, vm-proxy
│   │
├── ┬── Lab / Proto
│   │   ├── fw-lab
│   │   │   └── Isolé, pas de LAN, accès sortant restreint
│   │   └── vm-sandbox, vm-test
│   │
├── ┬── DNS / AdGuard Home
│   │   ├── fw-dns
│   │   │   └── INPUT 53/443 seulement, DoH vers upstream DNS
│   │   └── vm-dns
│   │
├── ┬── Dump + Encryption Zone 🧷 (Nouvelle zone)
│   │   ├── fw-dump
│   │   │   ├── INPUT : trafic de logs, télémétrie, fichiers
│   │   │   └── OUTPUT : VPN only (chiffrement avant sortie)
│   │   └── vm-dump
│   │       ├── Collecte (rsyslog, beats, netflow, tcpdump, journaux apps)
│   │       ├── Chiffrement (GPG, LUKS, Age, etc.)
│   │       └── Envoi off-site (Nextcloud, Rclone, SSHFS via VPN)
│   │
├── ┬── NIDS/NIPS Central (collecte)
│   │   └── vm-nids
│   │       ├── Suricata/Snort branché via port mirroring/tap
│   │       ├── NIPSec active sur segments utilisateurs
│   │       └── Alerting vers vm-admin
│   │
└── ┬── Backup Zone 💾
    │   ├── fw-backup
    │   │   ├── INPUT : autorisé seulement depuis certains VMs internes
    │   │   └── OUTPUT : interdit (Air-gapped logique)
    │   └── vm-backup
            ├── Stockage chiffré (Borg, Restic, rsync, ZFS snapshots)
            ├── Accès en pull uniquement
            └── Pas de service tournant inutile




minimal linux: reduce attack surface: void Linux
