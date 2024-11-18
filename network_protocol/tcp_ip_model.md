TCP/IP 모델에 따르면. 네트워크 프로토콜은 4계층으로 이루어진다.
### **1. Link Layer**

The link layer represents the physical and data link technologies that enable the transmission of data across a network. Examples include:

- **Ethernet**
- **Wi-Fi**
- **Bluetooth**

It handles the actual movement of data between devices in the same network and prepares it for higher layers.

---

### **2. Internet Layer**

This layer is responsible for transferring data between networks and determining the best path for delivery. Common protocols include:

- **IP (Internet Protocol)**: Handles addressing and routing of packets.
- **ICMP (Internet Control Message Protocol)**: Used for error reporting and diagnostics (e.g., `ping`).
- **ARP (Address Resolution Protocol)**: Resolves IP addresses to physical MAC addresses.

---

### **3. Transport Layer**

The transport layer ensures reliable or fast communication between devices. Key protocols are:

- **TCP (Transmission Control Protocol)**: Reliable, connection-oriented communication.
- **UDP (User Datagram Protocol)**: Fast and lightweight, suitable for real-time communication, but less reliable.
- Other protocols include **RUDP, RDDP**, which are less commonly used.

---

### **4. Application Layer**

The application layer provides services that directly interact with users or applications. It includes protocols for various purposes:

- **HTTP**: Web browsing.
- **FTP**: File transfers.
- **SMTP**: Email communication.
- **DNS**: Domain name resolution.
