# IoT-IPv6-Analysis_Mon-IoT-or
#### Submitted by: Shubham Santosh Upadhyay<br>
#### Guided by: Prof. David Choffnes, Dr. Daniel J. Dubois<br>
-----------------------------------------------------------------------------------------
# Description
Analyze if an IoT device behaves differently when deployed on an IPv6 network with respect to an IPv4 network.

Problem statement: 
Analyze if an IoT device behaves differently when deployed on an IPv6 network with respect to an IPv4 network

# Goals: 
#### (Establish) Having an IPv6 network and ensuring that IoT devices work
#### (Scale) Collecting traffic from all the devices connected to IPv6
#### (Experiment) Analyzing the traffic from a Mac address
-----------------------------------------------------------------------------------------
# (Establish) Having an IPv6 network and ensuring that IoT devices work
Methodology:
- configure tunnel/interfaces for IPv6-IPv4 communication.
- As part of configuring the network for IPv6-IPv4 communication, Radvd was configured to enable IPv6 on its own VM
- Test communication between the IPv6 network and the devices 	to ensure that the tunneling and Radvd configurations were working correctly
- Check connection of different IoT devices on the ipv6 network

Why these Results:
- Compatibility assessment: The results help you identify which devices are compatible with   
  IPv6 networks and which are not.
- Identifying potential issues: The results provide insight into potential problems, such as 
  software or hardware compatibility issues, that might occur when deploying IPv6 on a larger scale.
- Performance benchmarking: As you scale up the experiment, having baseline data on the 
  performance of devices operating on an IPv6 network
- Confidence in scaling up

#### Learnings:
#### These can be scaled up to perform the experiment in the lab
------------------------------------------------------------------------------------------
# (Scale) Collecting traffic from all the devices connected to IPv6
Methodology:
- Device readiness: Double-check that all devices are running the latest firmware, software 
  updates, and patches to ensure compatibility with the IPv6 network.
- Network configuration: Verify that the routers, switches, and other network components are 
  properly configured to handle IPv6 traffic.
- Traffic monitoring setup: Deploy monitoring tools, Tshark (in this case), at strategic 
  points in the network to capture traffic from all devices.
- Data collection: Start the monitoring tools and capture traffic data for a 2-hour period

Results:
We have a pcap file with all the traffic from the IoT devices in the lab.
Why these results?
Real-world representation: A larger-scale experiment better simulates real-world scenarios
Compatibility evaluation: Scaling up allows for a comprehensive assessment of device compatibility
Performance benchmarking: A scaled-up experiment provides more reliable performance data, enabling better comparisons
#### Learnings:
#### Now that we have a pcap file and the devices are communicating, with a list of Mac addresses we can identify the behavior and do the comparison. 
--------------------------------------------------------------------------------------------
# (Experiment) Analyzing the traffic from a Mac address
Methodology:
- A huge pcap file is segmented into smaller one
- Mac address from the list of devices is taken
- The mac address is passed through the code and output is obtained

Interesting observation from the output:
- A mix of IPv4 (0.0.0.0) and IPv6 (::, fe80::, 2001:) addresses is used for source and 
  destination IPs. This indicates a dual-stack network with both IPv4 and IPv6 capabilities. 
  The reason for using dual-stack is to ensure backward compatibility with older IPv4-only 
  devices while taking advantage of IPv6's larger address space and improved routing features.
- Most of the traffic involves link-local (fe80::) or multicast (ff02::, ff05::*) IPv6 
  addresses, particularly for ICMPv6 and UDP protocols. Link-local addresses are used for 
  communication within a local subnet, while multicast addresses are used for one-to-many or 
  many-to-many communication within a local or larger network scope. The reason for this 
  observation could be that the table captures traffic related to local network management, 
  discovery, or neighbor solicitation.
- A significant portion of traffic uses ICMPv6 protocol, which is responsible for diagnostic 
  and control messages in IPv6 networks. This could include neighbor solicitation and 
  advertisement messages or route solicitation and advertisement messages.
- There are several instances of traffic with protocol '0'. In this table, '0' might represent 
  a placeholder for an unknown or unsupported protocol.
- Some traffic involves Google Public DNS servers (2001:4860:4860::8888 and 
  2001:4860:4860::8844) over ICMPv6 and UDP protocols. This suggests that devices in the 
  network are using Google's DNS servers for domain name resolution.
- A few TCP connections are established with 2607:f8b0:4006:80a::200a and 
  2607:f8b0:4004:c17::bc, which are IPv6 addresses owned by Google. This might indicate that 
  devices in the network are communicating with Google services like Google Search, Google 
  Drive, or Google Cloud Platform.
- Additionally, it is communicating with 2001:470:20::2, which is a DNS server provided by 
  Hurricane Electric.
----------------------------------------------------------------------------------------------
# Future Work:

- We have done the analysis of just one or two Mac addresses, furthermore caparisons can be 
  made in order to understand the relative behavior of IoT devices
- More network traffic pcap files can be captured under different circumstances in order to 
  See the IoT connections
- The code to analyze the traffic for a particular mac address can be improved by adding more 
  functionalities
- Still, the security aspects provided by the ipv6 can be explored


