# Firewalld

## Objective

Verify that the Firewalld service is installed, running, and configured as the system's active firewall.

---

## Why Firewalld?

Firewalld is the default firewall management service on Rocky Linux. It dynamically manages firewall rules using predefined zones and services to help protect the system from unauthorized network access.

---

## 1. Verify Firewalld Service

Check the status of the Firewalld service:

```bash
sudo systemctl status firewalld
```

Verify that the service is **active (running)**.

<img align="center" src="../../screenshots/firewall status.png" alt="Rocky Linux Installation" width="700" />

## 2. Verify Firewall State

Display the current firewall state:

```bash
sudo firewall-cmd --state
```

Expected output:

```text
running
```

This confirms that Firewalld is currently active.

## 3. Display Active Zone

Show the active firewall zone:

```bash
sudo firewall-cmd --get-active-zones
```

This command displays the active zone and the network interface(s) assigned to it.

## 4. Display Current Configuration

List the active firewall configuration:

```bash
sudo firewall-cmd --list-all
```

Review the configured zone, enabled services, open ports, and other active firewall settings.

<img align="center" src="../../screenshots/firewall config.png" alt="Rocky Linux Installation" width="700" />

## Summary

Verified the following:

- Firewalld is installed and running.
- The firewall service is active.
- The active firewall zone was identified.
- The current firewall configuration was successfully displayed.