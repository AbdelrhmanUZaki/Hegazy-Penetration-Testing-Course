
# Why We Need to Scan Ports with Nmap

Before performing penetration testing on a server, we must gather information about its open ports. Understanding the open ports is crucial because:

1. **Identify Details**: The ports reveal specific information about the running services on the server.
2. **Service Availability**: A port usually indicates that a service is running and accessible.
3. **User Access**: Open ports allow users to connect to and utilize the service hosted on the server.

## Importance of Nmap

In some cases, critical ports like 7001 (often used by Java developers for debugging) can be hidden. Without a port scanner like Nmap, you may not discover such ports. If you identify an open port with Nmap, you can potentially exploit it and gain control over the server.

## Understanding Port Status

- **Open Port**: You can interact with the service running on it.
- **Closed Port**: A service is configured on the port but currently not running.
- **Filtered Port**: A firewall or filtering device is preventing access to the port.

## Key Ports to Consider

Critical ports like MySQL’s default port 3306 should be protected with a firewall to prevent unauthorized access.

By default, Nmap scans the top 1000 commonly used ports, such as HTTP (port 80), HTTPS (port 443), and SMTP (port 25).

## Dealing with Non-Standard Ports

While SSH typically runs on port 22, a developer might configure it on an uncommon port like 22222. A basic Nmap scan may miss this unless you perform a full scan of all 65,535 ports.

## Example: Ping Scan

A ping scan can quickly identify live hosts within specific IP ranges:

```bash
nmap -v -sn 192.168.0.0/16 10.0.0.0/8
```

This command sends ICMP echo requests across the specified ranges. If an IP responds, there is likely an active server. However, keep in mind that some servers may be configured to block ping requests.

## Advanced Scanning: Virtual IPs and SNMP

### Virtual IP (VIP)

A Virtual IP (VIP) is an IP address that is not tied to a specific physical device. Instead, it can be used by multiple devices, typically in a load balancing or high availability setup. VIPs are commonly used in scenarios where you want to ensure uninterrupted access to services, even if one of the servers goes down. For example, in a load balancing cluster, a VIP can be assigned to the cluster as a whole, allowing traffic to be automatically redirected to healthy nodes.

VIPs are also used in high availability setups like HAProxy and keepalived, where they help in failover mechanisms.

### SNMP (Simple Network Management Protocol)

SNMP is a protocol used for monitoring and managing devices on a network. It operates on UDP port 161. SNMP can be used to retrieve and modify configuration settings on systems, routers, switches, and other network devices. It plays a critical role in network administration, as it provides a standardized way to collect data, monitor performance, and manage configurations.

In penetration testing, if you can gain access to an SNMP service with weak credentials, you might be able to retrieve sensitive information or even change system configurations. 

```bash
nmap -sT -sU <target>
```

- `-sT`: Scans TCP ports.
- `-sU`: Scans UDP ports.

During a scan, pressing `Space` will show the progress percentage.

## Scanning the Top N Ports

To scan the top N most popular ports:

```bash
nmap -sT -sU --top-ports 2000 <target>
```
The number `2000` is the Eng. Ebrahem Hegazi choice.  
Scanning all 65,535 ports on production systems is not recommended because:
- It takes considerable time.
- It places significant load on the server.
- It could potentially trigger a denial of service (DoS) via a TCP flood.

## Example: Scanning Specific Ports

```bash
nmap -p 80,443 <target>
```

## Dealing with Firewalls

A common firewall on Linux distributions is `iptables`. To list all configured rules:

```bash
iptables -L
```

Common rules may include:
- Blocking specific ports.
- Allowing only certain IP addresses to access a port.
- Allowing a range of IP addresses.

## Scanning All Ports

To perform a comprehensive scan of all TCP and UDP ports:

```bash
nmap -sT -sU -p 1-65535 <target>
```

This will result in scanning `2*65,535` ports (one set for TCP and another for UDP), creating significant network traffic.

## Analyzing Unknown Ports with Nmap’s `-A` Option

If you discover an unfamiliar port and don’t recognize its service, use the `-A` switch:

```bash
nmap -p 80,443 -A <target>
```

The `-A` switch sends multiple payloads to determine the service. It tries connecting as various types of servers (e.g., SSH, FTP) to analyze responses. If Nmap returns `tcpwrapped`, it indicates that the service is difficult to identify.

This option also provides additional details, like HTTP methods supported by a web server, or the server type. Such information might even lead to discovering a subdomain takeover vulnerability.

## Tasks
- Study Nmap switches and options to improve scanning techniques.
