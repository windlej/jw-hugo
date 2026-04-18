---
title: "The Lab"
description: "Enterprise-grade homelab built on free and open-source software. Everything tested here before it hits the blog."
layout: "single"
---

## Philosophy

Everything on this site gets tested on real gear before it's published. I don't write about how something *should* work. I write about how it *actually* works, including what breaks and how I fixed it.

The software stack is entirely free and open source. Proxmox VE instead of vSphere (for the cluster), OPNsense instead of commercial firewalls (for software firewall labs), TrueNAS Scale for storage, GNS3 and EVE-NG for network topologies. The physical gear is secondhand enterprise equipment.

---

## Compute

| Device | Specs | Role |
|---|---|---|
| Dell PowerEdge R630 | 2× Xeon E5-2680 v4 · 256GB RAM · 4× 10GbE | Primary hypervisor host (Proxmox) |
| HP ProLiant DL380 Gen9 | 2× Xeon E5-2690 v3 · 192GB RAM · 4× 10GbE | Secondary hypervisor host (Proxmox) |

Both servers are connected to a 10GbE switch trunk for vMotion and storage traffic. iDRAC (R630) and iLO (DL380) provide out-of-band management.

---

## Networking

| Device | Role |
|---|---|
| Cisco ASA 5516-X | Perimeter firewall · VPN · ACL labs |
| Cisco 3750G Stack (2U) | Core switching · VLANs · STP · inter-VLAN routing · SVIs |
| Cisco ASR 1002 *(planned)* | WAN simulation · BGP · MPLS labs |
| Unifi AP | Wireless for management network |

The physical network gear is the backbone of all Cisco CLI lab content. The 3750G runs IOS 12.2(55)SE, which covers CCNA switching exam topics directly.

---

## VLAN Design

| VLAN | Name | Subnet | Purpose |
|---|---|---|---|
| 1 | Native | — | Untagged / unused |
| 10 | Servers | 10.0.10.0/24 | Hypervisor management, VMs |
| 20 | Lab-Net | 10.0.20.0/24 | General lab workloads |
| 30 | Management | 10.0.30.0/24 | OOB management (iDRAC, iLO) |
| 40 | GNS3-Bridge | 10.0.40.0/24 | GNS3/EVE-NG cloud node integration |
| 99 | Storage | 10.0.99.0/24 | iSCSI / NFS storage traffic |

---

## Software Stack

All free and open source unless noted.

| Tool | Purpose |
|---|---|
| **Proxmox VE** | Hypervisor cluster (replacing vSphere) · Ceph for shared storage |
| **OPNsense** | Software firewall VM · micro-segmentation labs |
| **TrueNAS Scale** | NAS · iSCSI shared datastore for Proxmox |
| **Proxmox Backup Server** | VM backup · incremental forever · deduplication |
| **GNS3** | Virtual network lab · Cisco IOSv · ASAv topologies |
| **EVE-NG Community** | Multi-vendor virtual lab · Juniper · Fortinet · Cisco |
| **Wazuh** | Open source SIEM · custom detection rules · endpoint agents |
| **Windows Server 2022** | Active Directory · DNS · DHCP · Group Policy |
| **Ubuntu Server 22.04** | Linux workloads · Netmiko/Ansible control node |

---

## Virtual Lab Integration

GNS3 and EVE-NG topologies connect to the physical network via a **Cloud node** bridged to VLAN 40 (GNS3-Bridge). This means:

- Virtual routers in GNS3 can exchange routes with the physical Cisco 3750G
- Physical VMs in Proxmox can reach virtual hosts in GNS3 topologies
- Lab scenarios can test real physical-to-virtual integration, not just isolated simulations

This is the setup that makes content like "BGP from a GNS3 router to a physical switch" possible.

---

## Planned Additions

- **Cisco ASR 1002** — WAN simulation, BGP labs, eventually MPLS
- **Additional 10GbE switch** — dedicated storage fabric for Ceph replication
- **Raspberry Pi cluster** — lightweight automation control plane experiments
- **XCP-ng node** — side-by-side hypervisor comparison content

---

## What Gets Tested Here

Every blog post and video that involves a lab environment was built and tested in this setup before publication. That includes:

- All GNS3 and EVE-NG topology configs
- All Proxmox and TrueNAS procedures
- All Netmiko, Ansible, and Python network automation scripts
- All OPNsense firewall policies
- All Windows Server and Active Directory procedures
