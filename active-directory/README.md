# Active Directory Lab

A simulated Windows corporate environment for practising internal network penetration testing techniques including enumeration, lateral movement, and privilege escalation.

---

## Architecture

```
┌─────────────────────────────────────────┐
│           Host Machine (Windows 11)     │
│         Hypervisor: [VMware/VirtualBox] │
│                                         │
│  ┌──────────────┐   ┌────────────────┐  │
│  │   DC01       │   │  Workstation01 │  │
│  │   Windows    │   │  Windows 10    │  │
│  │   Server     │   │  (Domain User) │  │
│  │   (Domain    │   │                │  │
│  │   Controller)│   │                │  │
│  └──────┬───────┘   └───────┬────────┘  │
│         │                   │           │
│         └─────────┬─────────┘           │
│                   │                     │
│          ┌────────┴────────┐            │
│          │   Kali Linux    │            │
│          │  (Attack Box)   │            │
│          └─────────────────┘            │
│                                         │
│         Internal Network:               │
│         192.168.x.0/24                  │
└─────────────────────────────────────────┘
```

---

## Machines

| VM | OS | Role | IP |
|----|----|------|----|
| DC01 | Windows Server 2019 | Domain Controller | 192.168.x.10 |
| WS01 | Windows 10 | Workstation (domain-joined) | 192.168.x.11 |
| Kali | Kali Linux | Attack Machine | 192.168.x.20 |

---

## Setup Guide

### 1. Domain Controller (DC01)

- Install Windows Server 2019 (evaluation ISO — free from Microsoft)
- Promote to Domain Controller
- Domain name: `corp.local`
- Create users, groups, and intentional misconfigurations for practice

### 2. Workstation (WS01)

- Install Windows 10 (evaluation ISO — free from Microsoft)
- Join to `corp.local` domain
- Log in as a domain user (not admin)

### 3. Attack Machine (Kali)

- Standard Kali Linux installation
- Set network adapter to same internal network as DC01 and WS01

### 4. Intentional Misconfigurations (for practice)

- [ ] Kerberoastable service accounts
- [ ] ASREPRoastable accounts (no pre-auth required)
- [ ] SMB signing disabled on workstations
- [ ] Weak passwords on service accounts
- [ ] Unconstrained delegation
- [ ] Local admin reuse across workstations

---

## Attack Techniques Practised

- [ ] Network enumeration (Nmap, NetExec)
- [ ] SMB enumeration
- [ ] LDAP enumeration (ldapdomaindump, BloodHound)
- [ ] Kerberoasting
- [ ] ASREPRoasting
- [ ] Pass-the-Hash
- [ ] Pass-the-Ticket
- [ ] DCSync
- [ ] BloodHound path analysis

---

## Tools Used

| Tool | Purpose |
|------|---------|
| BloodHound | AD relationship mapping and attack path analysis |
| Impacket | Collection of Python scripts for AD attacks |
| NetExec (nxc) | Network authentication testing |
| Rubeus | Kerberos attacks |
| Mimikatz | Credential extraction (in lab only) |
| CrackMapExec | SMB enumeration and attacks |

---

## References

- [TCM Security — Practical Ethical Hacking (AD section)](https://tcm-sec.com)
- [HackTheBox Academy — Active Directory](https://academy.hackthebox.com)
