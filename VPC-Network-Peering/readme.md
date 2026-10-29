# TECHNICAL LOG & BGP ENGINEERING GUIDE

## VPC PEERING
**CCNP Miguelangel Luna**

---

## CONTENIDOS:

| Case | Title | Description |
| :--- | :--- | :--- |
| **01** | [Claude & n8n AI Agents](./case-01-Google-Auth/) | Agentes Claude . |


[Google](https://www.google.com)

## 1. Introduction and Theoretical Framework



## 2. Topology and BGP Neighbor Establishment


![BGP WEIGTH](images/01Topologia.jpg)

 

## 3. BGP Configuration:

**Task 1: Create a Custom Network in Both Projects:**

Within the same organization node, a network can host services that need to be accessible from other VPC networks in the same or different projectsAlternatively, an organization may want to access services offered by a third-party provider.

Project names are unique across all of Google Cloud, so you do not need to specify the organization when setting up peering. Google Cloud identifies the organization based on the project name.

In this lab, you have been provisioned two projects: the first project is `project-A`, and the second is `project-B`.

**1.1** In each project, start a new Cloud Shell session by clicking the **+** icon.
**1.2** In the Cloud Shell for `project-A`, set the project ID for `project-A`:

```text
gcloud config set project Project ID 1
```

```text
gcloud config set project Project ID 2
```
### Project A

**1.3** Return to the first Cloud Shell tab and run the following command to create a custom network:

```text
gcloud compute networks create network-a --subnet-mode custom
```

**1.4** Create a subnet within this VPC and specify a region and IP range by running:
  
```text
gcloud compute networks subnets create network-a-subnet --network network-a \
    --range 10.0.0.0/16 --region "REGION 1"
```

**1.5**  Create a VM instance:

```text
gcloud compute instances create vm-a --zone "ZONE 1" --network network-a --subnet network-a-subnet --machine-type e2-small
```
**1.6** Run the following command to enable SSH and ICMP, as you will need a secure shell to communicate with VMs during connectivity testing:

```text
gcloud compute firewall-rules create network-a-fw --network network-a --allow tcp:22,icmp
```

**Next you set up Project-B in the same way..**

### 4. BGP Configuration:

