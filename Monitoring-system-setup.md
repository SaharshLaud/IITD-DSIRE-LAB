# LibreNMS Monitoring System Setup for SNMP on Ubuntu Server

This guide provides the necessary steps to enable SNMP (Simple Network Management Protocol) on an Ubuntu server to facilitate monitoring through LibreNMS.

## Prerequisites
- A running Ubuntu server.
- SSH access to the server.
- LibreNMS server configured to monitor SNMP-enabled devices.

## Step 1: Install the SNMP Daemon and Utilities

### 1.1 Log in to the Manager Server
First, connect to the manager server via SSH as a non-root user:

```bash
$ ssh your_username@manager_server_ip_address
```

### 1.2 Update the System
Update your system's package index:

```bash
$ sudo apt update
```

### 1.3 Install SNMP Daemon and Utilities
Install the SNMP daemon (`snmpd`) and the required utilities:

```bash
$ sudo apt install snmpd
```

## Step 2: Configure SNMP Daemon

### 2.1 Edit SNMP Configuration File
You need to configure the SNMP daemon by editing the `snmp.conf` and `snmpd.conf` files. Open the `snmp.conf` file using a text editor:

```bash
$ sudo nano /etc/snmp/snmp.conf
```

Then open the `snmpd.conf` file:

```bash
$ sudo nano /etc/snmp/snmpd.conf
```

### 2.2 Modify the Configuration File
Make necessary changes to the `snmpd.conf` file:

```bash
# sysLocation    Sitting on the Dock of the Bay
# sysContact     Me <me@example.org>
# sysServices    72
# agentAddress  udp:127.0.0.1:161

# Uncomment or add the following lines:

# Define read-only community string and allowed IP addresses
rocommunity cse!005 10.208.20.30

# Define the SNMP agent listening addresses
agentAddress udp:161,udp6:[::1]:161

# Define SNMP extensions
extend distro /usr/bin/distro
extend hardware "/bin/cat /sys/devices/virtual/dmi/id/product_name"
extend manufacturer "/bin/cat /sys/devices/virtual/dmi/id/sys_vendor"

# Set system location and contact information
sysLocation   Block 2
sysContact    apawar.cstaff@cc.iitd.ac.in
```

> **Note**: Ensure that you replace `cse!005` and `10.208.20.30` with your own SNMP community string and allowed IP address, respectively. Customize `sysLocation` and `sysContact` as per your requirements.

### 2.3 Save and Exit
After making the necessary changes, save the file and exit the text editor.

## Step 3: Allow SNMP Ports Through the Firewall

### 3.1 Allow UDP Port 161 and 162
To ensure SNMP traffic can reach your server, configure your firewall to allow UDP ports 161 and 162.

```bash
$ sudo ufw allow 161/udp
$ sudo ufw allow 162/udp
```

## Step 4: Restart the SNMP Daemon

Finally, restart the SNMP daemon to apply the changes:

```bash
$ sudo /etc/init.d/snmpd restart
```

This will restart the SNMP service and apply the configuration changes.

## Conclusion

Your server is now configured to allow SNMP monitoring. You can proceed to integrate it with LibreNMS for detailed monitoring. Make sure your LibreNMS server is set up with the correct SNMP community string and IP address to begin monitoring the server.
