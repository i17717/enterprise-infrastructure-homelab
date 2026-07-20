# System Update

## Objective

Update the operating system to the latest available packages and apply security patches before deploying additional services.

## Why Updates Matter

Keeping the system up to date ensures:

- Latest security patches
- Bug fixes and stability improvements
- Updated kernel and system packages
- Compatibility with future software

## 1. Verify Current System Version

Display the operating system information:

```bash
cat /etc/os-release
```

Display the installed kernel version:

```bash
rpm -q kernel
```

## 2. Check for Available Updates

Refresh the package metadata and check for available updates:

```bash
sudo dnf check-update
```

This command checks configured repositories and lists packages that can be updated without installing them.

---

## 3. Update Installed Packages

Install all available package updates:

```bash
sudo dnf update
```

## 4. Reboot the System

Restart the server if a new kernel or critical system packages were updated.

```bash
sudo reboot
```

A reboot ensures the system loads the latest kernel and applies all updates.

## 5. Verify the Update

Verify the running kernel:

```bash
uname -r
```

Confirm that no updates remain:

```bash
sudo dnf check-update
```
