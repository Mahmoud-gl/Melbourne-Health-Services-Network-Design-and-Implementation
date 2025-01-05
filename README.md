# Melbourne Health Services Network Design and Implementation

## Overview
Melbourne Health Services is implementing a new network infrastructure for its headquarters (HQ) and branch hospital. The goal is to establish a secure, cost-effective, and reliable network that ensures the confidentiality, integrity, and availability of data. The network design includes multiple departments at both locations, with distinct VLANs and subnets for each department. 
The HQ will host critical servers such as DHCP, DNS, Web, and Email servers, while both locations will be interconnected with core routers, multilayer switches for inter-VLAN routing, and access switches.
## Network Design Requirements

1. **Network Topology**:
   - **HQ and Branch Locations**: The network is divided into two main locations: the HQ (Headquarters) and the branch hospital. 
   - **Core Routers**: Both HQ and Branch will have a core router connected to the internet via two ISPs.
   - **Access Switches**: Each department at HQ and the Branch will have access switches connecting to a multilayer switch (MLS) that facilitates inter-VLAN routing.
   - **Wireless Network**: Every department will have its own wireless network for users.

2. **VLAN Design**:
   - Each department will be assigned its own VLAN and subnet.
   - The base IP network `192.168.100.0` will be subnetted to allocate the appropriate number of IP addresses for each department.
   - Estimated users per department: 60 users at HQ, 30 users at the Branch.

3. **Server-Side Site**:
   - The server-side will be located at HQ and will host the DHCP server, DNS server, Web server, and Email server.
   - Devices in the server room will use static IP addresses.

4. **Routing and Security**:
   - OSPF will be used for routing.
   - Extended ACLs and IPSec VPN will be implemented to secure communication between HQ and the Branch.
   - SSH will be configured on routers and switches for remote management.
   - Port security will be enabled for the server room switch to allow only one device per port.

5. **Additional Configurations**:
   - **PAT**: To enable devices to access the internet, Port Address Translation (PAT) will be configured using the respective outbound router interface.
   - **Static Routing**: Default static routing will be configured for forwarding traffic that does not match routing table entries.
   - **DHCP**: Devices in each department will obtain IP addresses dynamically from the DHCP servers in the server room.

## Detailed Steps for Configuration

### 1. **Network Design**
   - **VLAN Assignment**: Create VLANs for each department and assign appropriate subnets from `192.168.100.0/24`.
     - Example:
       - MLOCS: VLAN 10, Subnet: `192.168.10.0/25`
       - MER: VLAN 20, Subnet: `192.168.20.0/25`
       - MRM: VLAN 30, Subnet: `192.168.30.0/25`
       - IT: VLAN 40, Subnet: `192.168.40.0/25`
       - CS: VLAN 50, Subnet: `192.168.50.0/25`
       - NSO: VLAN 60, Subnet: `192.168.60.0/25`
       - HL: VLAN 70, Subnet: `192.168.70.0/25`
       - HR: VLAN 80, Subnet: `192.168.80.0/25`
       - MK: VLAN 90, Subnet: `192.168.90.0/25`
       - FIN: VLAN 100, Subnet: `192.168.100.0/25`

### 2. **Network Configuration in Cisco Packet Tracer**
   - Use Cisco Packet Tracer to create the network topology as per the design.
   - Configure devices (routers, multilayer switches, access switches) and interconnect them as specified.

### 3. **Device Configuration**
   - **Basic Device Settings**:
     - Hostname, console password, enable password, and banner messages.
     - Disable IP domain lookup.
   
   - **Configure Multilayer Switches for Inter-VLAN Routing**:
     - Assign IP addresses to VLAN interfaces.
     - Enable routing on multilayer switches.
   
   - **Configure OSPF**:
     - Configure OSPF on both routers and multilayer switches to advertise routes.
   
   - **Configure DHCP**:
     - Set up the DHCP server on the server-side site to allocate IP addresses dynamically to devices in all departments.
   
   - **SSH Configuration**:
     - Enable SSH for secure remote login on routers and switches.
   
### 4. **Security Configuration**
   - **Access Control Lists (ACLs)**:
     - Implement extended ACLs to restrict access based on security requirements.
   
   - **VPN Configuration**:
     - Configure IPSec VPN to create a secure tunnel for communication between HQ and the Branch.
   
   - **Port Security**:
     - Configure port security on the server room switch to allow only one device per port using the sticky MAC address method.
   
   - **PAT Configuration**:
     - Configure Port Address Translation (PAT) on the routers for outbound traffic.
   
### 5. **Testing and Validation**
   - Verify communication between devices in different VLANs.
   - Test inter-site communication via VPN.
   - Check IP address allocation from DHCP.
   - Test internet access for all devices through PAT.
   - Ensure port security is working by verifying device connection limits.

---


---

## Conclusion

This network design and implementation project ensures Melbourne Health Services has a secure, reliable, and cost-effective network infrastructure that meets its operational and security requirements.
By following this plan, the company can confidently manage and protect its data while enabling smooth and efficient communication across both the HQ and branch locations.


