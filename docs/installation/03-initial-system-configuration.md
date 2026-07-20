# Initial System Configuration

## Objective

Prepare a freshly installed Rocky Linux server for administration.

## Prerequisites

- Rocky Linux installed
- Logged in as root (first boot)
- Network connectivity available

## 1. Verify System Information

Verify the operating system, hostname, and kernel version.

### Display system information

```bash
hostnamectl
```

Displays the hostname, operating system, kernel version, architecture, and virtualization information.

### Display OS release

```bash
cat /etc/os-release
```
Shows detailed information about the installed operating system.

### Display kernel version

```bash
uname -r
```
Displays the currently running Linux kernel.

<img align="center" src="../../screenshots/system-info.png" alt="Rocky Linux Installation" width="700" />

## 2. Configure Hostname

Assign a meaningful hostname to identify the server.

```bash
hostnamectl set-hostname ei-core
```

Verify the change:

<img align="center" src="../../screenshots/new-hostname.png" alt="Rocky Linux Installation" width="700" />

## 3. Create an Administrative User

Create a dedicated administrator account instead of using `root` for daily tasks.

Create the user:

```bash
useradd lilli
```

Set a password:

```bash
passwd lilli
```

Grant administrative privileges:

```bash
usermod -aG wheel lilli
```

Verify group membership:

```bash
id lilli
```

<img align="center" src="../../screenshots/group membership.png" alt="Rocky Linux Installation" width="700" />

## 4. Configure sudo Access

Switch to the new user:

```bash
su - lilli
```

Verify administrative privileges:

```bash
sudo whoami
```

Expected output:

```text
root
```

<img align="center" src="../../screenshots/root acces.png" alt="Rocky Linux Installation" width="700" />

## 5. Verify Network Connectivity

Display network interfaces:

```bash
ip addr
```

Display the routing table:

```bash
ip route
```

Test Internet connectivity:

```bash
ping -c 4 8.8.8.8
```

Test DNS resolution:

```bash
ping -c 4 google.com
```

<img align="center" src="../../screenshots/network connectivity.png" alt="Rocky Linux Installation" width="700" />

## 6. Verify Time Settings

Display current date, time, and synchronization status.

```bash
timedatectl
```

(Optional) Configure the timezone:

```bash
timedatectl set-timezone Africa/Khartoum
```

Verify:

```bash
timedatectl
```

<img align="center" src="../../screenshots/time setting.png" alt="Rocky Linux Installation" width="700" />

## Summary

Completed the following tasks:

- Verified system information
- Configured the hostname
- Created an administrative user
- Verified `sudo` access
- Verified network connectivity
- Verified DNS resolution
- Verified system time settings