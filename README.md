# Network_analysis-tool

This Python script is built to help analyze and monitor network traffic by reading a PCAP file. It can detect security threats like **port scanning**, **ARP spoofing**, and **DNS spoofing**. The script makes use of **Scapy** for packet analysis, **pandas** for working with data, and logs its findings to help you keep track of what’s going on.

 Key Features:

1. **Libraries Used**:
   - **sys**: For handling system-level stuff like exiting the program if things go wrong.
   - **logging**: To log important info and warnings so we can keep an eye on things.
   - **Scapy**: The core tool that lets us read, process, and manipulate network packets from the PCAP file.
   - **pandas**: Organizes packet data into neat tables so we can analyze it easily.
   - **tabulate**: Helps print out the data in a clean, readable table format.
   - **tqdm**: Adds a nice progress bar so you know how long the packet processing will take.

---

### Function Breakdown:

1. **`read_pcap(pcap_file)`**:
   - Reads the PCAP file using Scapy’s `rdpcap()` function. If the file’s missing or there's an error, it logs an error and stops the program.

2. **`extract_packet_data(packets)`**:
   - Pulls out key info like source IP, destination IP, protocol type, and packet size. All this data gets stored in a pandas DataFrame for easy analysis.

3. **`protocol_name(number)`**:
   - Translates protocol numbers (like TCP = 6, UDP = 17) into names we recognize like TCP, UDP, or ICMP.

4. **`analyze_packet_data(df)`**:
   - This is the core of the analysis. It calculates:
     - **Total Bandwidth**: Adds up the size of all packets.
     - **Protocol Distribution**: How much of the traffic is TCP, UDP, ICMP, etc.
     - **IP Communication Patterns**: Looks for the busiest IP pairs (who’s talking to whom the most).
     - **Protocol Frequency**: Counts how many times each protocol shows up.
   - It returns this data, which we’ll later print out.

5. **`extract_packet_data_security(packets)`**:
   - Same as `extract_packet_data()`, but it also logs destination ports, which is key for detecting **port scans**.

6. **`detect_port_scanning(df, port_scan_threshold)`**:
   - This checks for port scanning behavior. If an IP is sending packets to a lot of different ports, more than a set threshold, it could be up to something fishy like a port scan.

7. **`detect_arp_spoof(packet)`**:
   - Looks for signs of **ARP spoofing**. If an IP address shows up with a new MAC address, we’ll raise a red flag.

8. **`detect_dns_spoof(packet)`**:
   - Watches out for **DNS spoofing** by checking if a domain suddenly resolves to a new IP address, which could be suspicious.

9. **`print_results()`**:
   - Once all the analysis is done, it prints the results:
     - Total bandwidth used.
     - Protocol breakdown.
     - Who’s talking to who (IP communication patterns).

10. **`main()`**:
    - The main function that ties everything together:
      - Reads the PCAP file.
      - Extracts and analyzes both traffic data and security data.
      - Detects any possible threats.
      - Prints out all the results for you.

---

### How It Works:

1. **Step 1: Read the PCAP File**:
   - The script kicks off by reading the provided **PCAP** file. This file contains all the network traffic data that’s been captured.

2. **Step 2: Extract & Analyze the Data**:
   - **Data Extraction**: Pulls out the key details from the network packets like source/destination IPs, the protocol used (TCP, UDP, etc.), and the size of each packet.
   - **Data Analysis**: 
     - Calculates total bandwidth usage.
     - Identifies the most common protocols in the traffic.
     - Highlights which IPs are communicating the most.

3. **Step 3: Detect Security Issues**:
   - **Port Scanning Detection**: Checks if any IP addresses are trying to communicate with a lot of different ports, which could be a sign of port scanning.
   - **ARP Spoofing Detection**: For ARP packets, it watches for IP addresses being tied to different MAC addresses than usual.
   - **DNS Spoofing Detection**: Keeps an eye out for domain names that start resolving to different IP addresses.

4. **Step 4: Print the Results**:
   - Finally, the script prints out the total bandwidth used, protocol distribution, and the top IP communications in a clean table format.

---

### Use Cases:
- **Network Traffic Analysis**: Get a clear view of your network’s bandwidth, protocol use, and IP communication patterns.
- **Port Scanning Detection**: Spot malicious activity where someone might be scanning your network for open ports.
- **Spoofing Detection**: Keep an eye out for **ARP** or **DNS spoofing** attacks that can lead to serious security issues.

### Conclusion:
This tool is great for not only understanding your network traffic but also for detecting potential threats. Whether it’s catching a **port scan** or **spoofing attempts**, it’s got your back for making sure your network stays secure.

--- 
