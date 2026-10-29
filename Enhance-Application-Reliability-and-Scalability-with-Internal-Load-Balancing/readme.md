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

## Overview: Google Cloud Internal Load Balancing (ILB)

Google Cloud's Internal Load Balancing (ILB) is a crucial service for managing and scaling your private application infrastructure. It enables you to distribute TCP/UDP-based traffic efficiently across internal virtual machine instances, ensuring your applications are highly available and performant within your private network. By providing a single, stable private IP address for your services, ILB simplifies internal application communication and enhances system resilience.

In this lab, you will set up an internal service by creating two managed instance groups in the same region, representing a common deployment pattern for highly available applications. Next, you will configure and thoroughly test an Internal Load Balancer, using these instance groups as its backends. This setup mimics a real-world scenario where an internal application—such as a microservice, an API endpoint, or a database—needs to be accessible to other internal services or applications without exposure to the public internet.


## 2. Topology and BGP Neighbor Establishment

![BGP WEIGTH](images/01Topologia.jpg)


## Configuration:

**R:**

```text

```

### Configuration:


