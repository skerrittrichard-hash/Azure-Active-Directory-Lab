# VM Creation & Setup

## Overview

DC-1 stands for Domain Controller. This VM serves as the central identity and access management system for my lab environment. The purpose is to:
- Train and familiarize myself with Azure infrastructure
- Demonstrate my ability to deploy and administer Windows Server VMs
- Showcase hands-on Active Directory administration skills

## Virtual Machine Specifications

| Specification | Value | Details |
|--------------|-------|---------|
| Computer Name | DC1 | Domain Controller |
| Operating System | Windows Server 2022 Datacenter | Enterprise-grade server OS |
| VM Size | Standard B2as v2 | 2 vCPUs, 8 GiB RAM |
| VM Generation | V1 | Azure VM architecture |
| VM Architecture | x64 | 64-bit processor |
| Region | UK South West | Closest available to UK East |
| Disk | 1 OS disk | 127GB storage |

## Why These Choices?

### Operating System: Windows Server 2022 Datacenter

Windows Server 2022 Datacenter was selected to create an enterprise-realistic learning environment, rather than using the minimal Standard edition. This ensures the lab reflects real-world infrastructure decisions and provides a more authentic platform for learning Active Directory administration.

### VM Size: Standard B2as v2

The B2as v2 size (2 vCPUs, 8GB RAM) represents the sweet spot for an enterprise-realistic lab environment:
- **Sufficient for AD:** Active Directory requires adequate RAM to handle objects, authentication requests, and directory operations efficiently
- **Cost-effective for labs:** Provides realistic performance without excessive cost on free tier
- **Scalable thinking:** While this size is suitable for a small company environment, larger enterprises would scale to larger VM sizes (B4ms, D-series, or higher) based on user count and organizational needs
- **Better than minimal:** Choosing B2as v2 over a smaller B1s demonstrates understanding that infrastructure sizing matters

### Region: UK South West

Selected UK South West because:
- I am based in the UK (East Yorkshire)
- UK East was the preferred region for lowest latency, but was unavailable
- UK South West is the next closest available region
- This demonstrates understanding of region selection in cloud infrastructure (latency and proximity matter)

## Networking Configuration

### Public IP Address: 20.117.8.104

**Purpose:** Enables remote access to DC1 from the internet via Remote Desktop Protocol (RDP)

**Why it's needed:**
- Without a public IP, I cannot connect to the VM remotely from my home
- The public IP acts as the entry point for RDP connections
- This is secured by Network Security Group (NSG) firewall rules

**Security consideration:** A public IP is acceptable with proper security controls (NSG rules, monitoring, strong credentials)

### Private IP Address: 10.0.0.4

**Purpose:** Used for internal communication within the Azure virtual network

**Details:**
- Allows DC1 to communicate with other VMs on the same virtual network (DC1-vnet)
- This is the internal network address used by domain-joined computers and users
- Private IP addresses are not routable on the internet

### Virtual Network: DC1-vnet/default

The VM is connected to the DC1-vnet virtual network with the default subnet configuration.

## Security & Storage Considerations

### Current Configuration (Home Lab)

| Setting | Status | Details |
|---------|--------|---------|
| Encryption at host | Disabled | Data not encrypted on physical host |
| Azure disk encryption | Not enabled | OS disk not encrypted |
| Auto-shutdown | Not enabled | VM can run continuously |
| Health monitoring | Not enabled | No performance monitoring |

### Production Recommendations

This configuration is **acceptable for a home lab** but would **NOT be acceptable in an enterprise environment**. For production deployment:

- **Enable "Encryption at host"** - Encrypts data on the physical Azure host
- **Enable "Azure disk encryption"** - Encrypts the OS disk
- **Implement backup and disaster recovery** - Protect against data loss
- **Enable health monitoring** - Track VM performance and health
- **Configure auto-shutdown** - Reduce costs and idle resource usage
- **Implement Azure Policy** - Enforce security and compliance standards

## Disk Configuration

- **OS Disk:** 1 managed disk (~127GB)
- **Additional Data Disks:** 0
- **Disk Type:** Standard managed disk (appropriate for lab environment)
