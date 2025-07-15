# Linux DNS and Web Server Configuration (Red Hat)

This project demonstrates how to set up and test a DNS server and web server on a Red Hat Linux virtual machine using BIND and Apache. It was completed as a group project for COP3350 – Systems Administration & Programming at FGCU.

## Project Overview

- Configured a working DNS server using BIND with forward and reverse lookup zones.
- Set up an Apache web server to host a basic HTML website locally.
- Verified domain resolution through loopback DNS queries and tested web server output in a browser.
- Managed firewall settings and virtual network configurations to support connectivity between services.

## Tools and Skills Used

- Red Hat Enterprise Linux (RHEL)
- BIND9 DNS Server
- Apache HTTP Server
- Bash / Linux Command Line
- VirtualBox and VM Networking
- DNS Zone File Configuration
- Basic HTML and Web Hosting
- Firewall and Port Configuration

## Setup Steps

### 1. Install DNS packages

```bash
sudo yum install bind* -y
```

### 2. Configure DNS

Edit the main config:

```bash
sudo nano /etc/named.conf
```

Add forward and reverse zone entries:

```bash
sudo nano /etc/named.rfc1912.zones
```

Example zone file paths:

```text
/var/named/exampledomain.com.zone
/var/named/10.0.0.rev
```

### 3. Start and test DNS server

```bash
sudo systemctl start named
sudo systemctl enable named
```

Test DNS resolution (loopback address):

```bash
dig @127.0.0.1 exampledomain.com
dig -x 10.0.0.1
```

### 4. Install and configure Apache

```bash
sudo yum install httpd -y
sudo nano /etc/httpd/conf/httpd.conf
```

Set the `ServerName` directive to a local test domain such as `exampledomain.com`.

Create or modify your HTML page:

```bash
sudo nano /var/www/html/index.html
```

### 5. Start and test Apache server

```bash
sudo systemctl start httpd
sudo systemctl enable httpd
```

Access the site in a browser using:

```text
http://localhost
http://<VM-IP-address>
```

### 6. Firewall configuration (if needed)

```bash
sudo firewall-cmd --add-port=53/udp --permanent
sudo firewall-cmd --add-port=53/tcp --permanent
sudo firewall-cmd --add-service=http --permanent
sudo firewall-cmd --reload
```

## Report

The full project report with configuration steps and testing results is located in:

```
report/Group3_ProjectReport.pdf
```

## Notes

This was a collaborative project completed using Red Hat virtual machines and local networking. Domain resolution and web access were tested within a controlled environment. This project reflects foundational experience in configuring and managing Linux-based network services and servers.

