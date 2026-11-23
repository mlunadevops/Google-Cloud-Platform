# TECHNICAL LOG & IMPLEMENTING CLOUD HA VPN IPSEC AND BGP PART 3/3

## GCP CLOUD HA GSP619
**CCNP Miguelangel Luna**

![Diagrama de VPN](/images/diagram.svg)

![End-to-End Hybrid Packet Flow](./images/01-hybrid-vpn-flow.svg)
---

## CONTENIDOS:

| Case | Title | Description |
| :--- | :--- | :--- |
| **01** | [Claude & n8n AI Agents](./case-01-Google-Auth/) | Agentes Claude . |

[Google](https://www.google.com)

## 1. Introduction and Theoretical Framework

**pyATS =** The infrastructure for organizing, running, and reporting automated network tests in a professional way.

## 2. Topology and BGP Neighbor Establishment

![BGP WEIGTH](images/01Topologia.png)

## 3. IMPLEMENTATION:

**1.1) Create the working folder and enter it::**

```text
python3 -m venv csr1kv
```

**Part 3:** Use the pyATS Testing Library

**3.1) Install pyATS**

Inside the virtual environment (make sure you see (csr1kv) in your terminal), run:

```text
pip3 install pyats[full]
```

**3.2) Verify the installation**

Verify that it was installed correctly by running:

```text
pyats --help
```

