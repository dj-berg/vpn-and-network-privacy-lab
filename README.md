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

By comparing the public IP address, network provider, and approximate geographic location at each stage, I was able to observe how internet traffic appears to originate from different networks depending on where the connection exits to the internet.

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

![Local public IP information](images/local-ip.png)

The initial lookup demonstrated that a public IP address can provide information about the network provider and approximate geographic location associated with an internet connection.

---

## ☁️ Part 2 — Deploying a Windows 11 Virtual Machine in Azure

Next, I created a virtual machine in Microsoft Azure to establish a remote Windows environment located in another geographic region.

The VM was configured with:

- **VM Name:** `vpn-test`
- **Resource Group:** `daniel`
- **Region:** Spain Central
- **Operating System:** Windows 11 Pro
- **VM Size:** `Standard_B2as_v2`
- **vCPUs:** 2
- **Memory:** 8 GiB

Hosting the virtual machine in Spain provided a remote environment whose network location could be compared with my local connection in Arizona.

### 📸 Azure Virtual Machine

![Azure Windows virtual machine](images/azure-vm.png)

---

## 🖥️ Part 3 — Connecting to the Azure VM

After the virtual machine was deployed, I obtained its public IP address and connected to the Windows 11 system using Remote Desktop.

This allowed me to control the Azure-hosted computer from my local machine while applications and web requests executed from the remote VM.

Before connecting to a VPN, Proton VPN identified the VM's connection as:

- **Country:** Spain
- **Provider:** Microsoft Azure
- **VPN Status:** Unprotected

### 📸 Azure VM Before VPN Connection

![Azure VM public IP before VPN](images/azure-vm-ip.png)

This demonstrated an important networking concept: although I was controlling the VM remotely from Arizona, internet activity performed inside the VM used the Azure VM's network connection in Spain rather than my local connection.

At this stage, the connection could be represented as:

```text
Local Computer
Tempe, Arizona
      │
      │ Remote Desktop
      ▼
Azure Windows 11 VM
Spain
      │
      ▼
   Internet
```

---

## 🔒 Part 4 — Connecting the VM to Proton VPN

With the Azure VM running in Spain, I installed the Proton VPN desktop application inside the Windows 11 environment.

After installing and signing into Proton VPN, I connected the VM to an available VPN server located in the **Netherlands**.

### 📸 Proton VPN Connection

![Proton VPN connected to Netherlands](images/proton-vpn.png)

The VPN client now reported the connection as **Protected**, confirming that the VPN tunnel had been established.

At this point, the Azure VM was still hosted in Microsoft's Spain Central region, but its internet traffic was being routed through the VPN server in the Netherlands.

---

## 🌍 Part 5 — Verifying the VPN Connection

After establishing the VPN connection, I returned to the IP lookup service from inside the Azure VM.

The public-facing network information had changed.

The lookup reported:

- **ISP:** WorldStream B.V.
- **Service:** VPN Server
- **City:** Naaldwijk
- **Region:** Zuid-Holland
- **Country:** Netherlands

### 📸 Public IP After VPN Connection

![Public IP after connecting to VPN](images/vpn-ip.png)

The IP lookup service also detected that the connection was using a VPN.

The Azure VM itself remained hosted in Spain, but external websites now identified the internet connection with the VPN server in the Netherlands.

The completed network path could be represented as:

```text
Local Computer
Tempe, Arizona
      │
      │ Remote Desktop
      ▼
Azure Windows 11 VM
Spain
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

The three stages produced different public-facing network information.

| Stage | Environment | Network / Provider | Approximate Location |
|---|---|---|---|
| 1 | Local Computer | Arizona State University | Tempe, Arizona, United States |
| 2 | Azure Windows 11 VM | Microsoft Azure | Spain |
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

Each environment presented a different public IP address and associated network and geographic information to external services.

---

## 🧠 Key Takeaways

### Public IP Addresses

A public IP address represents a network's internet-facing identity. External services can use public IP information to determine details such as the associated network provider and approximate geographic location.

### Remote Desktop & Cloud Networking

Connecting to a remote computer does not mean that the remote computer uses the local machine's public IP address for its own internet requests.

Although I controlled the Azure VM from Arizona using Remote Desktop, internet activity performed inside the VM used Microsoft's Azure infrastructure in Spain.

### VPN Connections

Connecting the Azure VM to Proton VPN changed the public IP address visible to external websites.

Instead of seeing the Azure VM's original Spanish network connection, websites observed the public-facing IP associated with the VPN server in the Netherlands.

### VPN Privacy

A VPN can mask the original public IP address from destination websites by routing internet traffic through a VPN server.

However, VPN usage does not provide complete anonymity. A VPN changes the network endpoint visible to destination services, but other technologies and account activity can still be used to identify or track users.

---

## 🔐 Security & Privacy Considerations

Sensitive information such as account passwords and authentication credentials was excluded from this repository.

When documenting IT environments, credentials and other sensitive information should never be stored in source code, documentation, or public GitHub repositories.

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
└── images/
    ├── azure-vm-ip.png
    ├── azure-vm.png
    ├── local-ip.png
    ├── proton-vpn.png
    └── vpn-ip.png
```

---

## 📚 Project Summary

This project provided hands-on experience with public IP addressing, cloud-hosted virtual machines, Remote Desktop, and Virtual Private Networks.

Starting from a local connection in Arizona, I deployed and remotely accessed a Windows 11 virtual machine hosted in Microsoft Azure's Spain Central region. I then connected the VM to a VPN server in the Netherlands and compared the public-facing network information at each stage.

The lab demonstrated how the network through which internet traffic exits affects the public IP address, network provider information, and approximate geographic location observed by external services.
