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

- From Cloud Shell, create a VPC network called `vpc-demo`:

```text
! 
gcloud compute networks create vpc-demo --subnet-mode custom
!


