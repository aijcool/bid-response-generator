# Infrastructure Sizing Template

## Document Information

| Field | Value |
|-------|-------|
| Project Name | {{projectName}} |
| Client | {{clientName}} |
| Version | 1.0 |
| Date | {{date}} |

---

## 1. Executive Summary

This document provides detailed infrastructure sizing for {{projectName}}, covering production and non-production environments.

### 1.1 Environment Overview

| Environment | Purpose | Users |
|-------------|---------|-------|
| Production | Live system | {{productionUsers}} |
| Staging | Pre-production testing | {{stagingUsers}} |
| Development | Development and testing | {{devUsers}} |
| DR | Disaster recovery | N/A |

### 1.2 Total Resource Summary

| Resource | Production | Non-Production | Total |
|----------|------------|----------------|-------|
| CPU Cores | {{prodCPU}} | {{nonProdCPU}} | {{totalCPU}} |
| Memory (GB) | {{prodMemory}} | {{nonProdMemory}} | {{totalMemory}} |
| Storage (TB) | {{prodStorage}} | {{nonProdStorage}} | {{totalStorage}} |

---

## 2. Production Environment

### 2.1 Application Servers

| Component | vCPU | Memory | Storage | Qty | Total vCPU | Total Memory |
|-----------|------|--------|---------|-----|------------|--------------|
| API Gateway | 4 | 8 GB | 50 GB | 2 | 8 | 16 GB |
| Web Server | 4 | 8 GB | 50 GB | 3 | 12 | 24 GB |
| App Server | 8 | 32 GB | 100 GB | 3 | 24 | 96 GB |
| Agent Engine | 16 | 64 GB | 200 GB | 2 | 32 | 128 GB |
| **Subtotal** | | | | **10** | **76** | **264 GB** |

### 2.2 Database Servers

| Component | vCPU | Memory | Storage | Qty | Total vCPU | Total Memory |
|-----------|------|--------|---------|-----|------------|--------------|
| PostgreSQL Primary | 16 | 64 GB | 500 GB | 1 | 16 | 64 GB |
| PostgreSQL Replica | 16 | 64 GB | 500 GB | 2 | 32 | 128 GB |
| Redis Cache | 8 | 32 GB | 100 GB | 3 | 24 | 96 GB |
| Elasticsearch | 8 | 32 GB | 500 GB | 3 | 24 | 96 GB |
| **Subtotal** | | | | **9** | **96** | **384 GB** |

### 2.3 Infrastructure Services

| Component | vCPU | Memory | Storage | Qty | Total vCPU | Total Memory |
|-----------|------|--------|---------|-----|------------|--------------|
| Load Balancer | 4 | 8 GB | 50 GB | 2 | 8 | 16 GB |
| Monitoring | 4 | 16 GB | 200 GB | 1 | 4 | 16 GB |
| Log Aggregator | 4 | 16 GB | 500 GB | 1 | 4 | 16 GB |
| **Subtotal** | | | | **4** | **16** | **48 GB** |

### 2.4 Production Total

| Resource | Value |
|----------|-------|
| Total Servers | 23 |
| Total vCPU | 188 |
| Total Memory | 696 GB |
| Total Storage | 4.5 TB |

---

## 3. Non-Production Environments

### 3.1 Staging Environment (50% of Production)

| Component | vCPU | Memory | Storage | Qty |
|-----------|------|--------|---------|-----|
| API Gateway | 2 | 4 GB | 25 GB | 1 |
| Web Server | 2 | 4 GB | 25 GB | 2 |
| App Server | 4 | 16 GB | 50 GB | 2 |
| Agent Engine | 8 | 32 GB | 100 GB | 1 |
| PostgreSQL | 8 | 32 GB | 250 GB | 1 |
| Redis Cache | 4 | 16 GB | 50 GB | 1 |
| Elasticsearch | 4 | 16 GB | 250 GB | 1 |
| **Subtotal** | | | | **9** |

### 3.2 Development Environment (25% of Production)

| Component | vCPU | Memory | Storage | Qty |
|-----------|------|--------|---------|-----|
| All-in-One Dev | 16 | 64 GB | 500 GB | 2 |
| Database | 8 | 32 GB | 250 GB | 1 |
| **Subtotal** | | | | **3** |

### 3.3 DR Environment (100% of Production - Passive)

| Component | vCPU | Memory | Storage | Qty |
|-----------|------|--------|---------|-----|
| Same as Production | - | - | - | 23 |

---

## 4. Storage Requirements

### 4.1 Storage by Type

| Type | Production | Staging | Dev | DR | Total |
|------|------------|---------|-----|-----|-------|
| SSD (High IOPS) | 2.0 TB | 1.0 TB | 0.5 TB | 2.0 TB | 5.5 TB |
| NVMe (Database) | 1.5 TB | 0.5 TB | 0.25 TB | 1.5 TB | 3.75 TB |
| HDD (Archive) | 1.0 TB | 0.5 TB | 0.25 TB | 1.0 TB | 2.75 TB |
| **Total** | **4.5 TB** | **2.0 TB** | **1.0 TB** | **4.5 TB** | **12.0 TB** |

### 4.2 Backup Storage

| Backup Type | Retention | Storage Estimate |
|-------------|-----------|------------------|
| Daily Full | 7 days | 31.5 TB |
| Weekly Full | 4 weeks | 18 TB |
| Monthly Full | 12 months | 54 TB |
| **Total Backup** | | **103.5 TB** |

---

## 5. Network Requirements

### 5.1 Bandwidth

| Connection | Bandwidth | Purpose |
|------------|-----------|---------|
| Internet Uplink | 1 Gbps | User access |
| Internal Network | 10 Gbps | Service communication |
| Storage Network | 25 Gbps | Database and storage |
| DR Replication | 100 Mbps | Data replication |

### 5.2 IP Addressing

| Environment | Subnet | IPs Required |
|-------------|--------|--------------|
| Production | /24 | 50 |
| Staging | /25 | 25 |
| Development | /26 | 15 |
| Management | /27 | 10 |

---

## 6. Procurement Summary

### 6.1 Server Hardware

| Item | Specification | Qty | Unit Price | Total |
|------|---------------|-----|------------|-------|
| App Server | 2U, 32-core, 256GB RAM | 10 | $15,000 | $150,000 |
| DB Server | 2U, 64-core, 512GB RAM | 6 | $25,000 | $150,000 |
| GPU Server | 4U, AI accelerated | 2 | $50,000 | $100,000 |
| **Subtotal** | | **18** | | **$400,000** |

### 6.2 Storage

| Item | Capacity | Qty | Unit Price | Total |
|------|----------|-----|------------|-------|
| All-Flash Array | 50TB | 2 | $100,000 | $200,000 |
| Backup Appliance | 200TB | 1 | $80,000 | $80,000 |
| **Subtotal** | | **3** | | **$280,000** |

### 6.3 Network

| Item | Description | Qty | Unit Price | Total |
|------|-------------|-----|------------|-------|
| Core Switch | 100GbE | 2 | $30,000 | $60,000 |
| Access Switch | 25GbE | 4 | $10,000 | $40,000 |
| Load Balancer | HA Pair | 1 | $50,000 | $50,000 |
| Firewall | HA Pair | 1 | $40,000 | $40,000 |
| **Subtotal** | | | | **$190,000** |

### 6.4 Total Infrastructure Cost

| Category | Cost |
|----------|------|
| Servers | $400,000 |
| Storage | $280,000 |
| Network | $190,000 |
| Software Licenses | $100,000 |
| Installation & Config | $50,000 |
| **Grand Total** | **$1,020,000** |

---

## Notes

- All sizing based on estimated {{productionUsers}} concurrent users
- Prices are estimates and subject to vendor quotes
- DR environment assumes passive standby configuration
- Cloud alternative pricing available upon request
