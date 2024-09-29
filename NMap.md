![NMap Logo](/assets/images/nmaplogo.jpeg)
# NMap

## What should you be looking for in particular using NMap.
When using **Nmap** (Network Mapper), it helps to know what you are trying to achieve. Nmap is a powerful tool for network discovery, security auditing, and identifying potential vulnerabilities. Here are key things to look for in particular, depending on your use case:

### 1. **Open Ports**
   - **What to look for**: Nmap will show you a list of open ports on a target. You should be looking for ports that are open unnecessarily, as they could be potential entry points for attackers.
   - **Why it matters**: Open ports provide entry points into systems, and if services running on these ports are vulnerable, they can be exploited.
   - **Command**: 
     ```
     nmap <target>
     ```
     Example output:
     ```
     PORT    STATE  SERVICE
     22/tcp  open   ssh
     80/tcp  open   http
     443/tcp open   https
     ```

### 2. **Service and Version Detection**
   - **What to look for**: Nmap can detect the specific services running on open ports (e.g., Apache web server, SSH daemon) and even their versions.
   - **Why it matters**: Knowing the exact service and version can help identify known vulnerabilities associated with that software version.
   - **Command**:
     ```
     nmap -sV <target>
     ```

### 3. **Operating System Detection**
   - **What to look for**: Nmap can attempt to identify the operating system running on the target machine.
   - **Why it matters**: If you're auditing a system, knowing the OS can help guide further investigation, such as looking for specific OS vulnerabilities.
   - **Command**:
     ```
     nmap -O <target>
     ```

### 4. **Potential Vulnerabilities**
   - **What to look for**: Using scripts, Nmap can perform deeper vulnerability scanning by testing for specific security issues.
   - **Why it matters**: Nmap scripting engine (NSE) can be used to check for well-known vulnerabilities or misconfigurations.
   - **Command**:
     ```
     nmap --script vuln <target>
     ```
     Example:
     ```
     PORT    STATE  SERVICE     VULNERABILITY
     443/tcp open   https       CVE-2014-3566 (POODLE SSL vulnerability)
     ```

### 5. **Firewall and Intrusion Detection**
   - **What to look for**: You can use Nmap to test if a target is behind a firewall or IDS (Intrusion Detection System).
   - **Why it matters**: If your scan results are showing a lot of closed or filtered ports, it may indicate that a firewall or IDS is present.
   - **Command**:
     ```
     nmap -sA <target>
     ```

### 6. **Network Topology (Traceroute)**
   - **What to look for**: Nmap can map out the route packets take to reach the target, helping you understand the network layout.
   - **Why it matters**: Traceroute can show the intermediate hops to a target, providing insights into the network infrastructure.
   - **Command**:
     ```
     nmap --traceroute <target>
     ```

### 7. **Host Discovery**
   - **What to look for**: Identify which hosts are online in a network.
   - **Why it matters**: This helps in understanding which systems are active and might need further investigation.
   - **Command**:
     ```
     nmap -sn <target>  # Performs a ping scan to identify live hosts
     ```

### 8. **Stealth Scanning**
   - **What to look for**: Use TCP SYN scan or other stealth scans to detect open ports without establishing a full connection.
   - **Why it matters**: Useful to bypass some firewalls or detection systems.
   - **Command**:
     ```
     nmap -sS <target>
     ```

### 9. **UDP Scanning**
   - **What to look for**: Nmap can also scan for open UDP ports, though it is slower and more resource-intensive.
   - **Why it matters**: Many critical services use UDP (e.g., DNS, DHCP), and open UDP ports can also be exploited.
   - **Command**:
     ```
     nmap -sU <target>
     ```

### 10. **Comprehensive Scanning**
   - **What to look for**: For more detailed audits, you can combine Nmap's capabilities to run a thorough scan.
   - **Why it matters**: This scan is useful for deep assessments where time and accuracy are important.
   - **Command**:
     ```
     nmap -A <target>
     ```

### 11. **Subnet Scanning**
   - **What to look for**: You can scan a full subnet to discover all live hosts and open ports in that subnet.
   - **Why it matters**: Useful for network mapping and discovering all systems in a given range.
   - **Command**:
     ```
     nmap <target>/24
     ```

### Best Practices:
   - Use Nmap from both internal and external network perspectives to get a holistic view of your environment.
   - Regularly scan critical systems to monitor for new open ports or vulnerabilities.
   - Be mindful of legal considerations when scanning networks that aren't owned by you.

What are you focusing on in your scans? I could tailor these suggestions even further.


## Creating a Report using NMap

To create a report using **Nmap**, you can export scan results in various formats, which makes it easy to document your findings. Here's a step-by-step guide on how to generate and format reports with Nmap.

### 1. **Basic Scan Output Redirection**
You can redirect Nmap's scan output directly to a file.

#### Command:
```bash
nmap <target> > scan_report.txt
```
This saves the output in **plain text** format in a file named `scan_report.txt`.

---

### 2. **Nmap Output Formats for Reporting**
Nmap supports several output formats that are useful for reporting. You can use these formats depending on how you want to present the data.

#### a. **Normal Output (-oN)**
The default output format, which is human-readable and contains scan details in text form.

#### Command:
```bash
nmap -oN report.txt <target>
```
- **Best for**: Simple reports that are easy to read by humans.

#### b. **XML Output (-oX)**
Generates output in XML format, which is machine-readable and can be imported into other tools for post-processing.

#### Command:
```bash
nmap -oX report.xml <target>
```
- **Best for**: When you need to feed the results into another tool or a custom report generator.

#### c. **Grepable Output (-oG)**
The output is in a format that’s easy to parse with grep or other command-line tools.

#### Command:
```bash
nmap -oG report.gnmap <target>
```
- **Best for**: Quick extraction and filtering of data from the scan results.

#### d. **All Output Formats (-oA)**
This saves the scan results in all available formats (normal, XML, and grepable).

#### Command:
```bash
nmap -oA my_report <target>
```
This will generate:
- `my_report.nmap` (Normal output)
- `my_report.xml` (XML output)
- `my_report.gnmap` (Grepable output)

- **Best for**: Comprehensive reporting with multiple formats for flexibility.

---

### 3. **Adding Additional Details to Reports**
You can include more specific scan details in your report for more in-depth analysis:

#### a. **Service and Version Detection (-sV)**
Add details about the services running on open ports.

```bash
nmap -sV -oN detailed_report.txt <target>
```

#### b. **Operating System Detection (-O)**
Add information about the operating system running on the target.

```bash
nmap -O -oN os_report.txt <target>
```

#### c. **Verbose Mode (-v)**
Increase the verbosity of the scan to include more details about the process.

```bash
nmap -v -oN verbose_report.txt <target>
```

#### d. **Script Scans and Vulnerability Detection (--script)**
Run Nmap scripts for vulnerability detection and include the results in the report.

```bash
nmap --script vuln -oN vuln_report.txt <target>
```

---

### 4. **Combining Output into a Custom Report**
Once you've generated your reports, you can combine the results into a more formal document. Here's how:

#### a. **Markdown Report**
You can format your report in **Markdown** for easy conversion to HTML or PDF.

Example:
```markdown
# Nmap Scan Report

## Target: 192.168.1.1

### Scan Summary:
- **Ports scanned**: 1-1000
- **Open ports**: 22 (SSH), 80 (HTTP)
- **Operating System**: Linux

### Detailed Results:
```bash
PORT    STATE  SERVICE  VERSION
22/tcp  open   ssh      OpenSSH 7.6p1
80/tcp  open   http     Apache httpd 2.4.29
```

---

#### b. **HTML Report Generation (Using External Tools)**
You can take the **XML output** and convert it to a more user-friendly format like **HTML** using external tools such as `xsltproc` or Nmap's own `ndiff` tool for comparisons.

1. **Convert XML to HTML** using `xsltproc`:
   ```bash
   xsltproc /usr/share/nmap/nmap.xsl report.xml > report.html
   ```

2. **Diff Reports** (to compare before-and-after scans):
   ```bash
   ndiff scan1.xml scan2.xml > comparison_report.txt
   ```

---

### 5. **Post-Processing with Other Tools**
You can use third-party tools to create more comprehensive or visual reports:

- **Zenmap**: Nmap’s GUI version, which also allows saving scans in XML or plain text format. You can visually interact with scan results and generate reports.

- **Nmap2Markdown**: A Python tool that converts Nmap XML output into Markdown format, which can easily be converted into PDF, HTML, or other formats.

---

### Sample Nmap Report Structure
Here's an example of how you can structure an Nmap report:

#### **Nmap Scan Report for 192.168.1.1**
1. **Scan Summary**:
   - **Date**: September 28, 2024
   - **Command**: `nmap -sV -O -oN report.txt 192.168.1.1`
   - **Host Status**: Up
   - **Latency**: 1.23 ms

2. **Open Ports**:
   - **Port 22 (SSH)**:
     - Service: OpenSSH
     - Version: 7.6p1
   - **Port 80 (HTTP)**:
     - Service: Apache
     - Version: 2.4.29
   - **Port 443 (HTTPS)**:
     - Service: Apache
     - Version: 2.4.29

3. **Operating System**:
   - Detected: Linux 3.x/4.x

4. **Vulnerability Summary**:
   - **CVE-2014-3566** (POODLE SSL Vulnerability)

5. **Recommendations**:
   - Close unnecessary open ports.
   - Update Apache to the latest secure version.
   - Disable vulnerable SSL protocols.

---

### Final Thoughts
To summarize, creating a report using Nmap involves:
1. Choosing the appropriate output format (`-oN`, `-oX`, `-oG`, `-oA`).
2. Adding details like version detection, OS detection, and scripts for vulnerabilities.
3. Formatting the output into a structured report using text editors or third-party tools.

Would you like more information on any specific tools or report formats?
