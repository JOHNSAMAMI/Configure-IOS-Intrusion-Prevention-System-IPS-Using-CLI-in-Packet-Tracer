# Configure-IOS-Intrusion-Prevention-System-IPS-Using-CLI-in-Packet-Tracer

Project Overview
This project involved configuring an Intrusion Prevention System (IPS) on a Cisco router to monitor and protect the 192.168.1.0 network from malicious traffic. The objective was to set up logging, modify IPS signatures, and verify the system's effectiveness in detecting and responding to threats.
Business Understanding
The implementation of an IPS is crucial for enhancing network security. By actively monitoring and blocking suspicious activities, organizations can protect sensitive data and maintain operational integrity. This project aimed to showcase the deployment and management of an IOS IPS in a simulated environment.
Tools and Frameworks Used
•	Packet Tracer: A network simulation tool for configuring Cisco devices.
•	Cisco IOS Commands: Used for router configuration.
Project Description
The project was executed in several stages, from enabling IPS on the router to testing its functionality. Below is a detailed breakdown of the tasks performed:
Topology and Addressing Table:
•	Configured routers (R1, R2, R3) and PCs, ensuring proper IP addressing and connectivity.
Objectives and Configuration Steps:
Part 1: Enable IOS IPS
Step 1: Enable the Security Technology Package
•	Verified the technology package status and enabled it if necessary.
R1(config)# license boot module c1900 technology-package securityk9
•	Accepted the end-user license agreement and saved the configuration.
Step 2: Verify Network Connectivity
•	Ping Tests: Verified successful connectivity between PC-C (192.168.3.2) and PC-A (192.168.1.2).
Step 3: Create an IPS Configuration Directory
•	Created a directory for IPS signatures in flash memory.
R1# mkdir ipsdir
Step 4: Configure IPS Signature Storage Location
•	Set the IPS signature storage location to the newly created directory.
R1(config)# ip ips config location flash:ipsdir
Step 5: Create an IPS Rule
•	Defined an IPS rule named iosips.
R1(config)# ip ips name iosips
Step 6: Enable Logging
•	Ensured syslog notifications were enabled and set up logging.
R1(config)# ip ips notify log
R1# clock set 10:20:00 10 january 2014
R1(config)# service timestamps log datetime msec
R1(config)# logging host 192.168.1.50
Step 7: Configure IPS Signature Categories
•	Modified the signature categories to retire all signatures and unretire the ios_ips basic category.
R1(config)# ip ips signature-category
R1(config-ips-category)# category all
R1(config-ips-category-action)# retired true
R1(config-ips-category-action)# exit
R1(config-ips-category)# category ios_ips basic
R1(config-ips-category-action)# retired false
Step 8: Apply the IPS Rule to an Interface
•	Applied the IPS rule to the G0/1 interface of R1 for outbound traffic.
R1(config)# interface g0/1
R1(config-if)# ip ips iosips out
________________________________________
Part 2: Modify the Signature
Step 1: Change the Event-Action of a Signature
•	Unretired and enabled the echo request signature (signature 2004, subsig ID 0), changing its action to alert and drop.
R1(config)# ip ips signature-definition
R1(config-sigdef)# signature 2004 0
R1(config-sigdef-sig)# status
R1(config-sigdef-sig-status)# retired false
R1(config-sigdef-sig-status)# enabled true
R1(config-sigdef-sig-engine)# event-action produce-alert
R1(config-sigdef-sig-engine)# event-action deny-packet-inline
Step 2: Use Show Commands to Verify IPS
•	Used the command show ip ips all to confirm the IPS configuration status. The iosips rule was applied on G0/1 outbound.
Step 3: Verify IPS Functionality
1.	From PC-C to PC-A: Attempted to ping PC-A. The pings were not successful due to the configured IPS blocking ICMP echo requests.
2.	From PC-A to PC-C: Attempted to ping PC-C. The pings were successful since the IPS configuration only blocked incoming ICMP echo requests from PC-C.
Step 4: View Syslog Messages
•	Accessed the Syslog server in Packet Tracer and checked the log file for IPS messages indicating blocked packets.
Step 5: Check Results
•	Confirmed that all tasks were completed successfully, achieving a 100% completion percentage.
________________________________________
Conclusion
The successful configuration of an IOS IPS on R1 demonstrated its capability to detect and mitigate specific threats, such as blocking unwanted ICMP echo requests while allowing legitimate traffic. The logging and monitoring setup provided insights into network security events, showcasing the effectiveness of proactive threat management.


