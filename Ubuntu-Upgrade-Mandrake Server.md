# Ubuntu Server Upgrade: From 16.04 to 18.04.6 LTS

This document provides a comprehensive guide to the **Ubuntu Server Upgrade** process performed on the **Mandrake** server at **IIT Delhi**, including handling of proxy settings, certificate errors, and broken packages.

## 1. Pre-Upgrade Steps

### 1.1 Backup and System State
- **Backup Data**: Ensure all important data and configurations are backed up
- **Check Current System State**: Verify the existing version and package state

```bash
lsb_release -a
sudo apt update
sudo apt upgrade -y
```

## 2. Resolving Proxy and Certificate Issues

### 2.1 Configure Proxy Settings
```bash
export http_proxy="http://proxy.example.com:8080"
export https_proxy="http://proxy.example.com:8080"
```

### 2.2 Update CA Certificates
```bash
sudo apt install --reinstall ca-certificates
```

### 2.3 Unset Proxy Settings
```bash
unset http_proxy https_proxy
```

## 3. Upgrading the Distribution

### 3.1 Update and Dist-Upgrade
```bash
sudo apt update
sudo apt dist-upgrade -y
```

### 3.2 Force Upgrade to 18.04
```bash
sudo do-release-upgrade -d
```

## 4. Resolving Issues During Upgrade

### 4.1 Handle Held or Broken Packages
```bash
sudo dpkg --configure -a
sudo apt --fix-broken install
```

### 4.2 Manually Upgrade Specific Packages
```bash
sudo apt list --upgradable
sudo apt remove package-name
sudo apt install package-name
```

## 5. Post-Upgrade Tasks

### 5.1 Verify the Upgrade
```bash
lsb_release -a
uname -r
```

### 5.2 Check for Broken Packages
```bash
sudo apt update
sudo apt -f install
```

### 5.3 Final System Upgrade
```bash
sudo apt full-upgrade -y
```

### 5.4 Clean Up Unused Packages
```bash
sudo apt autoremove -y
sudo apt clean
```

### 5.5 Reboot the System
```bash
sudo reboot
```

## 6. Final Check
```bash
lsb_release -a
sudo systemctl status <service-name>
```
