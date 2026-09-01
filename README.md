# 🔒 VPN & Network Privacy Lab

A hands-on networking lab exploring how public IP addresses, geographic network information, and internet traffic behavior change when using a cloud-hosted virtual machine and a Virtual Private Network (VPN).

In this project, I deployed a Windows 11 virtual machine in Microsoft Azure, connected to it remotely, compared public IP information across different network environments, and configured Proton VPN to observe how a VPN changes the public-facing network identity of a device.

---

## 🎯 Project Overview

The goal of this project was to better understand how public IP addresses identify internet connections and how VPNs affect the information visible to external websites.

The lab compared three different network states:

1. My local computer and network in Arizona
2. A Microsoft Azure virtual machine hosted in Spain
3. The same Azure virtual machine connected to a VPN server in the Netherlands

By comparing the public IP address, ISP/network provider, and approximate geographic location at each stage, I was able to observe how internet traffic appears to originate from different networks depending on where the connection exits to the internet.

---

## 🛠️ Technologies & Concepts

- Microsoft Azure
- Windows 11 Pro
- Azure Virtual Machines
- Remote Desktop Protocol (RDP)
- Proton VPN
- TCP/IP
- Public IP Addressing
- IP Geolocation
- Virtual Private Networks (VPNs)
- Network Connectivity
- Cloud Computing

---

## 🌐 Part 1 — Establishing a Local Network Baseline

Before creating the cloud environment, I checked the public IP information of my local computer using an IP lookup service.

The lookup identified the connection as originating from:

- **ISP:** Arizona State University
- **City:** Tempe
- **Region:** Arizona
- **Country:** United States

This established a baseline that could later be compared with the Azure virtual machine and VPN connections.

### 📸 Local Public IP Information

> **Screenshot 1 Placeholder — Local IP Lookup**
>
> `assets/images/01-local-ip.png`

<!-- Add Screenshot 1 here -->

The initial lookup demonstrated that a public IP address can provide information about the network provider and the approximate geographic location associated with an internet connection.

---

## ☁️ Part 2 — Deploying a Windows 11 Virtual Machine in Azure

Next, I created a virtual machine in Microsoft Azure to establish a remote Windows environment located in another geographic region.

The VM was configured with:

- **VM Name:** `vpn-test`
- **Resource Group:** `Daniel`
- **Region:** Spain Central
- **Operating System:** Windows 11 Pro
- **VM Size:** `Standard_B2as_v2`
- **vCPUs:** 2
- **Memory:** 8 GiB

Hosting the virtual machine in Spain provided a remote environment whose network location could be compared with my local connection in Arizona.

### 📸 Azure Virtual Machine

> **Screenshot 2 Placeholder — Azure VM Overview**
>
> `assets/images/02-azure-vm.png`

<!-- Add Screenshot 2 here -->

---

## 🖥️ Part 3 — Connecting to the Azure VM

After the virtual machine was deployed, I obtained its public IP address and connected to the Windows 11 system using Remote Desktop.

This allowed me to control the Azure-hosted computer from my local machine while applications and web requests executed from the remote VM.

Once connected, I opened the same IP lookup service from inside the Azure VM.

The connection was identified as:

- **ISP:** Microsoft Corporation
- **Service:** Data Center/Transit
- **City:** Madrid
- **Region:** Madrid
- **Country:** Spain

### 📸 Public IP from the Azure VM

> **Screenshot 3 Placeholder — Azure VM IP Lookup**
>
> `assets/images/03-azure-vm-ip.png`

<!-- Add Screenshot 3 here -->

This demonstrated an important networking concept: although I was controlling the VM remotely from Arizona, websites accessed from inside the VM saw the Azure VM's public-facing network connection in Spain rather than my local connection.

At this stage, the network path could be represented as:

```text
Local Computer
Tempe, Arizona
      │
      │ Remote Desktop
      ▼
Azure Windows 11 VM
Madrid, Spain
      │
      ▼
   Internet
```

---

## 🔒 Part 4 — Installing and Connecting to Proton VPN

With the Azure VM running in Spain, I installed the Proton VPN desktop application inside the Windows 11 environment.

After installing and signing into Proton VPN, I connected the VM to an available VPN server.

The VPN established a connection through a server located in the **Netherlands**.

### 📸 Proton VPN Connection

> **Screenshot 4 Placeholder — Proton VPN Connected**
>
> `assets/images/04-proton-vpn-connected.png`

<!-- Add Screenshot 4 here -->

At this point, the Azure VM was still physically hosted in Microsoft's Spain Central Azure region, but its internet traffic was now being routed through the VPN connection.

---

## 🌍 Part 5 — Verifying the VPN Connection

After establishing the VPN connection, I returned to the IP lookup service from inside the Azure VM.

The public-facing network information had changed.

The lookup now reported:

- **ISP:** WorldStream B.V.
- **Service:** VPN Server
- **City:** Naaldwijk
- **Region:** Zuid-Holland
- **Country:** Netherlands

### 📸 Public IP After Connecting to VPN

> **Screenshot 5 Placeholder — VPN IP Lookup**
>
> `assets/images/05-vpn-ip.png`

<!-- Add Screenshot 5 here -->

The Azure VM itself remained hosted in Spain, but external websites now identified the connection with the VPN server in the Netherlands.

The experiment now followed this path:

```text
Local Computer
Tempe, Arizona
      │
      │ Remote Desktop
      ▼
Azure Windows 11 VM
Madrid, Spain
      │
      │ VPN Connection
      ▼
VPN Server
Netherlands
      │
      ▼
   Internet
```

---

## 📊 Results

The three stages produced noticeably different public-facing network information.

| Stage | Environment | Network / ISP | Approximate Location |
|---|---|---|---|
| 1 | Local Computer | Arizona State University | Tempe, Arizona, United States |
| 2 | Azure Windows 11 VM | Microsoft Corporation | Madrid, Spain |
| 3 | Azure VM + Proton VPN | WorldStream B.V. / VPN Server | Naaldwijk, Netherlands |

The experiment demonstrated the progression:

```text
Local Network
Arizona, United States
       │
       ▼
Azure VM
Spain
       │
       ▼
VPN Server
Netherlands
```

Each environment presented a different public IP address and associated geographic/network information to external websites.

---

## 🧠 Key Takeaways

### Public IP Addresses

A public IP address represents a network's internet-facing identity. External services can use public IP information to determine details such as the associated ISP and approximate geographic location.

### Remote Desktop and Cloud Networking

Connecting to a remote computer does not mean that computer uses the local machine's public IP for its own internet requests.

Although I controlled the Azure VM from Arizona using Remote Desktop, websites accessed inside the VM identified its connection with Microsoft's Azure infrastructure in Spain.

### VPN Connections

Connecting the Azure VM to Proton VPN changed the public IP address visible to external websites.

Instead of seeing the Azure VM's original Spanish public IP, websites observed the public-facing IP associated with the VPN server in the Netherlands.

### VPN Privacy

A VPN can mask the original public IP address from destination websites by routing traffic through a VPN server.

However, VPN usage should not be confused with complete anonymity. A VPN changes which network endpoint is visible to destination services, but other technologies and account activity can still be used to identify or track users.

---

## 🧹 Part 6 — Resource Cleanup

After completing the experiment, I disconnected the VPN and cleaned up the Azure resources used for the lab.

Cloud virtual machines consume resources while operating, so shutting down, deallocating, or deleting resources that are no longer needed helps prevent unnecessary cloud costs.

### 📸 Azure Resource Cleanup

> **Screenshot 6 Placeholder — Azure Resources Stopped/Deleted**
>
> `assets/images/06-resource-cleanup.png`

<!-- Add Screenshot 6 here -->

Cleaning up temporary infrastructure is an important part of working responsibly with cloud environments.

---

## 🔐 Security & Privacy Considerations

Sensitive information has been excluded or redacted from this repository, including:

- Account passwords
- Authentication credentials
- Personal account information
- Full public IP addresses where unnecessary

Credentials should never be stored directly in source code, documentation, screenshots, or public GitHub repositories.

---

## 💡 Skills Demonstrated

- Microsoft Azure virtual machine deployment
- Windows 11 administration
- Remote Desktop connectivity
- VPN installation and configuration
- Public IP address identification
- IP geolocation analysis
- Cloud networking fundamentals
- VPN and network privacy concepts
- Network connectivity verification
- Cloud resource management

---

## 📁 Repository Structure

```text
vpn-and-network-privacy-lab/
│
├── README.md
│
└── assets/
    └── images/
        ├── 01-local-ip.png
        ├── 02-azure-vm.png
        ├── 03-azure-vm-ip.png
        ├── 04-proton-vpn-connected.png
        ├── 05-vpn-ip.png
        └── 06-resource-cleanup.png
```

---

## 📚 Project Summary

This project provided hands-on experience with public IP addressing, cloud-hosted virtual machines, Remote Desktop, and Virtual Private Networks.

Starting from a local connection in Arizona, I deployed and remotely accessed a Windows 11 virtual machine hosted in Microsoft Azure's Spain Central region. I then connected the VM to a VPN server in the Netherlands and compared the public-facing network information at each stage.

The lab demonstrated how the network through which internet traffic exits affects the public IP address, ISP information, and approximate geographic location observed by external services.
