# TECHNICAL LOG & Enterprise Multi-Region Hybrid Network Architecture using Google Cloud HA-VPN & Dynamic BGP Routing

## Enterprise Multi-Region Hybrid Network Architecture using Google Cloud HA-VPN & Dynamic BGP Routing

**CCNP Miguelangel Luna**

---

## CONTENT:

| Case | Title | Description |
| :--- | :--- | :--- |
| **01** | [Claude & n8n AI Agents](./case-01-Google-Auth/) | Agentes Claude . |

[Google Cloud Platform](https://www.google.com)

## 1. Introduction and Theoretical Framework



## 2. Topology and BGP Neighbor Establishment

The topology consists of four routers across different Autonomous Systems (AS 100, AS 200, AS 300, and AS 400). Before advertising prefixes, BGP neighbor adjacencies were established on each device.

![BGP WEIGTH](images/01Topologia.jpg)

 four routers across different Autonomous Systems (AS 100, AS 200, AS 300, and AS 400). Before advertising prefixes, BGP neighbor adjacencies were established on each device.

###  Task 1. Cloud VPC setup

- From Cloud Shell, create a VPC network called **`vpc-demo`**:

- **`vpc-demo`**: User-defined name to be assigned to the new VPC network.

- - **`--subnet-mode custom`**: Defines the subnet creation mode for this VPC, By choosing `custom` (custom mode), subnets are not created automatically in every region. This gives full control to manually decide which IP ranges (CIDR blocks) to assign, in which regions to create them, and how to structure your network topology (essential for enterprise environments and high-availability architectures like HA-VPN).

```text
gcloud compute networks create vpc-demo --subnet-mode custom
```


