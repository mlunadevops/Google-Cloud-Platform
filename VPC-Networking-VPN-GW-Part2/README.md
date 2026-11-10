# TECHNICAL LOG & IMPLEMENTING CLOUD HA VPN IPSEC AND BGP

## GCP CLOUD HA
**CCNP Miguelangel Luna**

---

## CONTENT:

| Case | Title | Description |
| :--- | :--- | :--- |
| **01** | [Claude & n8n AI Agents](./case-01-Google-Auth/) | Agentes Claude . |


[Google Skills](https://www.skills.google/)

An end-to-end hands-on demonstration of configuring, testing, and optimizing high-availability hybrid connectivity using **Google Cloud HA VPN** and dynamic BGP routing between Google Cloud VPCs and simulated on-premises environments.

---

## Architecture Overview (Topology) 

This project simulates a hybrid enterprise environment connecting a production VPC in Google Cloud (`vpc-demo`) to a remote simulated data center (`on-prem`) via Cloud HA VPN over public internet infrastructure.

```
+----------------------------------------+              +----------------------------------------+
|               vpc-demo                 |              |                on-prem                 |
|            (Region: us-west1)          |              |           (Region: us-west1)           |
|                                        |              |                                        |
|  Subnet: 10.1.2.0/24                   |              |  Subnet: 192.168.1.0/24                |
|  Cloud Router: vpc-demo-router1        |              |  Cloud Router: on-prem-router1          |
|  ASN: 65001                            |              |  ASN: 65002                            |
|                                        |              |                                        |
|         [ HA VPN Gateway ]             |<============>|         [ HA VPN Gateway ]             |
|         - Tunnel 0 (BGP Session 0)     |  IPsec Tunnels - Tunnel 0 (BGP Session 0)     |
|         - Tunnel 1 (BGP Session 1)     |              |  - Tunnel 1 (BGP Session 1)     |
+----------------------------------------+              +----------------------------------------+
```

![Topology](images/01Topologia.png)

---

## Technical Specifications

| Parameter | VPC Environment (vpc-demo) | VPC Environment (on-prem) |
| :--- | :--- | :--- |
| **VPC Region** | `us-west1` | `us-west1` |
| **VPN Tunnel name Interface 0** | `vpc-demo-tunnel0` | `on-prem-tunnel0` |
| **VPN Tunnel name Interface 1** | `vpc-demo-tunnel1` | `on-prem-tunnel1` |
| **Ike version** | 2 | 2 |
| **Shared secret** | `[SHARED_SECRET]` | `[SHARED_SECRET]` |
| **Router Name** | `vpc-demo-router1` | `on-prem-router1` |
| **VPN Gateway Name** | `vpc-demo-vpn-gw1` | `on-prem-vpn-gw1` |
---

## Implementation Steps (Configuration)

### 1. Prerequisites & VPC Preparation
Ensure both Google Cloud Virtual Private Clouds (VPCs) and their respective subnets are initialized:
* **Cloud VPC (`vpc-demo`)**: Contains workload subnets representing production infrastructure.
* **On-Prem VPC (`on-prem`)**: Represents external corporate network infrastructure.


### 2. VPN Gateway (Configuration):

![Topology](images/02VPNconfiguration.png)

**Creating VPN Gateways (vpc-demo-vpn-gw1):**

| CONFIGURACION VPN (vpc-demo-vpn-gw1) | CONFIGURACION VPN (on-prem-vpn-gw1) |
| :--- | :--- |
| `gcloud beta compute vpn-tunnels create vpc-demo-tunnel0 \`<br>`  --peer-gcp-gateway on-prem-vpn-gw1 \`<br>`  --region us-west1 \`<br>`  --ike-version 2 \`<br>`  --shared-secret [SHARED_SECRET] \`<br>`  --router vpc-demo-router1 \`<br>`  --vpn-gateway vpc-demo-vpn-gw1 \`<br>`  --interface 0` | `gcloud beta compute vpn-tunnels create on-prem-tunnel0 \`<br>`  --peer-gcp-gateway vpc-demo-vpn-gw1 \`<br>`  --region us-west1 \`<br>`  --ike-version 2 \`<br>`  --shared-secret [SHARED_SECRET] \`<br>`  --router on-prem-router1 \`<br>`  --vpn-gateway on-prem-vpn-gw1 \`<br>`  --interface 0` |****


![Gateway VPN output](images/05VPNGWoutput.png)

The command creates the following:
1. Two automatically assigned public IP addresses (The public IP addresses are ephemeral) on `interface0` and `interface1` for High Availability (HA).
2. The VPN Gateway connects to the VPC using GCP's Software-Defined Networking (SDN).


### 3. Cloud Router Configuration
Deploy Cloud Routers in both networks to manage dynamic BGP route exchanges.

**Cloud Router (`vpc-demo-router1`):**
```bash
gcloud compute routers create vpc-demo-router1 \
    --region us-west1 \
    --network vpc-demo \
    --asn 65001
```

**On-Prem Router (`on-prem-router1`):**
```bash
gcloud compute routers create on-prem-router1 \
    --region us-west1 \
    --network on-prem \
    --asn 65002
```

![Cloud router creation](images/06Cloudcreation.jpg)


## Key Features & Production Considerations
* **SLA Compliance**: Dual-tunnel layout achieves GCP's top 99.99% availability tier.
* **Dynamic Routing**: Uses BGP for automated path discovery, eliminating static routing risks.
* **Encrypted Transit**: All inter-site communication is encrypted end-to-end using IPsec.
