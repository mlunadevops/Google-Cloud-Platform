# TECHNICAL LOG & Creating an Internal TCP/UDP Load Balancer in Google Cloud

## Creating an Internal TCP/UDP Load Balancer in Google Cloud GSP216
**CCNP Miguelangel Luna**

---

An Internal TCP/UDP Load Balancer enables you to run and scale your services behind a private internal IP address that is accessible only to instances within the same VPC network, peered networks, or connected hybrid environments (via Cloud VPN or Interconnect).

---
### Architecture Overview

An internal load balancer consists of the following primary components:
1. **Health Check:** Monitors the availability and responsiveness of your backend virtual machine (VM) instances.
2. **Backend Service:** Defines how the load balancer distributes traffic to backend instances (based on region, protocol, and session affinity).
3. **Backend Instances:** Managed Instance Groups (MIGs) or unmanaged instance pools that process the traffic.
4. **Forwarding Rule:** Assigns a private internal IP address and port scope to receive incoming traffic and route it to the backend service.

---

### Step-by-Step Configuration Guide

#### Step 1: Create a Health Check
A health check probes your backend instances to ensure they are ready to receive traffic.

```bash
```


## CONTENT:

| Case | Title | Description |
| :--- | :--- | :--- |
| **01** | [Claude & n8n AI Agents](./case-01-Google-Auth/) | Agentes Claude . |

[Google](https://www.google.com)

## 1. Introduction and Theoretical Framework


## 2. Topology and BGP Neighbor Establishment

![BGP WEIGTH](images/01Topologia.jpg)


## 3. BGP Configuration:

**Router A (RTA - AS 100):**

```text

```

### Configuration:


