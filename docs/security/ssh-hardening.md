# SSH Hardening

## Objective

Improve the security of the SSH service by disabling direct root login and using a dedicated administrative account for remote administration.

### Why Harden SSH?

SSH is commonly used to remotely administer Linux servers. Restricting direct root access reduces the risk of unauthorized privileged access and improves accountability by requiring administrators to use individual accounts.

## 1. Verify SSH Service

Check that the SSH service is running:

```bash
sudo systemctl status sshd
```

## 2. Configure SSH

Edit the SSH server configuration file:

```bash
sudo vim /etc/ssh/sshd_config
```

Locate and modify the following directive:

```text
PermitRootLogin no
```

Save the file and exit the editor.

## 3. Validate the SSH Configuration

Before applying the changes, check the configuration for syntax errors:

```bash
sudo sshd -t
```

If the command produces no output, the configuration syntax is valid.

If an error is displayed, fix the configuration before reloading the SSH service.

## 4. Verify the Effective Configuration

Check the effective `PermitRootLogin` setting:

```bash
sudo sshd -T | grep permitrootlogin
```

Expected output:

```text
permitrootlogin no
```

This verifies the configuration that sshd will actually use.

## 5. Check Included Configuration Files

Rocky Linux may load additional SSH configuration files from:

```text
/etc/ssh/sshd_config.d/
```

If the effective configuration does not match the expected value, check these files:

```bash
sudo grep -Rni "PermitRootLogin" /etc/ssh/sshd_config /etc/ssh/sshd_config.d/
```

For example:

```text
/etc/ssh/sshd_config.d/01-permitrootlogin.conf:PermitRootLogin yes
```

If an included configuration file contains an incorrect setting, edit that file:

```bash
sudo vim /etc/ssh/sshd_config.d/01-permitrootlogin.conf
```

Change:

```text
PermitRootLogin yes
```

to:

```text
PermitRootLogin no
```

Then validate the configuration again:

```bash
sudo sshd -t
```

> **Note:** SSH configuration files can contain included settings, so checking the effective configuration with sshd -T is more reliable than checking only sshd_config.

## 6. Apply the Configuration

Once the configuration has been validated, reload the SSH service:

```bash
sudo systemctl reload sshd
```

Verify that the service remains active:

```bash
sudo systemctl status sshd
```

## 7. Verify Remote Access

From another machine, attempt to connect as root:

```bash
ssh root@192.168.56.101
```

The connection should be denied.

Then verify that the dedicated administrative account can connect:

```bash
ssh lilli@192.168.56.101
```

The administrative user should be able to log in and use sudo.

<img align="center" src="../../screenshots/disable root login.png" alt="Rocky Linux Installation" width="500" />

## Notes

- Always verify that an administrative user with `sudo` privileges can log in before disabling root SSH access.
- Consider using SSH key authentication instead of passwords in production environments.
- Additional hardening measures such as changing the default SSH port or disabling password authentication can be implemented later.
