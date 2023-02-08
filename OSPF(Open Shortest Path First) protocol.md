---

created: [ 2022-12-29 14:59 ]

updated_date: [ 29/12/2022 ]

tags: [ literature, ospf, dynamic routing protocols ]

---

# OSPF(Open Shortest Path First) protocol

Modified:: NaN

OSPF(Open Shortest Path First) protocol


# Notes
## Introduction and Concept of Open Shortest Path First OSPF
![[26-OSPF-Introducation.pdf ]]
- OSPF is a link state routing protocol, link means interface and state means status of the link which is cost. 
- How much cost is it to get to a destination
- Also a Dynamic routing protocol
- OSPF protocol uses IP protocol type 89 https://en.wikipedia.org/wiki/List_of_IP_protocol_numbers
	- Do not confuse with port number. They are not the same
- OSPF work out of AREA's. You cant have everything in 1 Area. Area 0 is the backbone. Area can be typed in 2 ways. A single digit or A.B.C.D format. 
- OSPF has Neighbor table, Topology table and Routing table. 
- OSPF supports trigger updates for fast convergence. 
- OSPF sends updates with sequence number. The number begins *0x80000001* and ends with *0x7FFFFFFF* Then it will start again
### OSPF Paket Multicast IP
![[multicast_ospf.png  | 900]]
### HELLO Packet Multicast IP
![[ospf_hello.png | 900]]
## Introduction and Concept of OSPF Protocol Terminologies![[27-OSPF-Terminologies.pdf]]
### AREA
- Area 0 is a must to configure in every OSPF configuration. 
- Area 0 is called the backbone. 
- Any Area that is not 0 is called *Area off Backbone* 
### ROUTER ID
- Router ID is unique to the router. 2 routers cannot have the same router id. You will get an error and the neighbor will not form. 
![[router_id.png | 1000]]
### LINK
- Link refers to the interface itself
### STATE
- State refers to the status of the interface i.e IP address, up/down status, subnet etc. 
### LSA
- The ( L ) stands for *LINK* and the ( S ) stands for *STATE* and the ( A ) stands for *ADVERTISEMENT*  (Do the math D.) 
### LSDB 
- Link State Database means all the informaion related to routing and the interface will be compliled into a database
### INTERNAL ROUTER
- Neighbor with router in same area
- All interfaces are in a single area
### DESIGNATED ROUTER/BACKUP DESIGNATED ROUTER
- Designated router is like the leader. All hellos are sent to the DR
- BDR is a backup for the DR
### ROUTER PRIORITY
- Tells who will become the DR or BDR
- Uses a value of 0-255 with a default value of 1
- A priority of 0 means that router will not participate in the election of DR/BDR
### AREA BORDER ROUTER
- Router with interfaces in more than one area
- Connects 2 areas together
### AUTONOMOUS SYSTEM BOUDARY ROUTER
- One interface running OSPF and another running another routing protocol.
	## OSPF Basic Configuration![[28-OSPF-Basic-Config.pdf ]]
	- OSPF used wildcard mask or inverse of subnetmask![[subnetting-cheat-sheet.pdf]]
	- If you are confused about the wildcard mask, you can go under the interface itself and configure OSPF. No network statement is needed if you have an IP address and subnetmask configured for that interface. OSPF will take the subnetmask and convert to wildcard itself. 
	- OSPF uses process ID, it can be any number. (1-65535)
	- Running the command `sh ip ospf interfaces` will display all interfaces running OSPF![[sh_ip_ospf_int.png]]
	- Running command `sh ip route ospf` will only show routes configured by ospf ![[sh_ip_ospf_route.png]]
### Conditions for OSPF Neighbor
1. Devices MUST be in same subnet
2. Connected interface MUST not be set to passive
	1.  Configuring an interface as *Passive* means no Hello's will be sent out of that interface. 
3. Same area
4. Hello and Dead intervals must match![[ospf_hello_timer.png | 950]]
5. Router ID must be unique
6. Same authentication configured. 
## OSPF Three Main Tables
![[29-OSPF-Tables.pdf]]
### OSPF Routing Table![[sh_ip_ospf_route1.png]]
### OSPF Neighbor Table
![[neighbor_table.png | 900]]
# Links