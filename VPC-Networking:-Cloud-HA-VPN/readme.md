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

**VPC:** is essentially your own **private IP address** space—an isolated virtual network environment—that has a global scope within your Google Cloud project. This allows any resource connected to it to communicate securely, **regardless of where in the world (region) that resource is physically located**.

Feactures:
- **Your own network block:** You decide which private IP ranges to use (for example, `10.0.0.0/16`) and how to divide them into subnets across different regions.
- **True global scope:** A VM in the `us-central1` (Iowa) region can communicate directly with a VM in `europe-west1` (Belgium) using their internal private IP addresses within the same VPC, **as if they were in the same building**.
- **Project-level scope:** By default, a **VPC belongs to a specific Google Cloud project** (although tools like Shared VPC exist if you need to share that same network with other projects in your organization).



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

### Task 2. Create subnets

- **`vpc-demo-subnet1`:** The name assigned to this specific new subnet (must be unique within that region and project).
- **`--network vpc-demo`:** Specifies the main VPC or parent network to which this subnet will belong (in this case, a network named **`vpc-demo`** that must already exist).
- **`--range 10.1.1.0/24`:** Defines the block of **private IP** addresses within this subnet. Here, you are reserving 256 IP addresses (ranging from `10.1.1.0` to `10.1.1.255`).
- **`--region "REGION 1"`:** Defines the geographical location (GCP region) where this subnet will be deployed (for example, `us-central1` or **`europe-west1`**, as subnets in GCP are regional).


1. Now, create subnet **`vpc-demo-subnet1`** in the **`REGION 1`** region:

```text
gcloud beta compute networks subnets create vpc-demo-subnet1 \
--network vpc-demo --range 10.1.1.0/24 --region "REGION 1"
```
### Create subnets

2. Create subnet **`vpc-demo-subnet2`** in the **`REGION 2`** region:

```text
gcloud beta compute networks subnets create vpc-demo-subnet2 \
--network vpc-demo --range 10.2.1.0/24 --region "REGION 2"
```

### Task 3. Create firewall rules for internal, SSH, and ICMP traffic:

- **`vpc-demo-allow-internal`**: The name assigned to this specific firewall rule (must be unique within the project).
- **`--network vpc-demo`:** Specifies the **target VPC network (**`vpc-demo`**) where this firewall rule will be enforced**.
- **`--allow tcp:0-65535,udp:0-65535,icmp`:** Defines what traffic is permitted by this rule:
  - **`tcp:0-65535`:** Allows all TCP ports from port 0 to 65535 (full TCP traffic).
  - **`udp:0-65535`:** Allows all UDP ports from 0 to 65535 (full UDP traffic).
  - **`icmp`:** Allows Internet Control Message Protocol traffic (used for tools like `ping`).
  - **Note:** Combined, this rule allows virtually all types of network traffic.
- **`--source-ranges 10.0.0.0/8`:** Defines where the traffic must come from for this rule to apply. In this case, it applies only to traffic originating from any IP address inside the `10.0.0.0/8` private network range (a very common internal corporate/cloud range).

```text
gcloud compute firewall-rules create vpc-demo-allow-internal \
  --network vpc-demo --allow tcp:0-65535,udp:0-65535,icmp --source-ranges 10.0.0.0/8
```

```text
gcloud compute firewall-rules create vpc-demo-allow-ssh-icmp \
  --network vpc-demo --allow tcp:22,icmp
```
