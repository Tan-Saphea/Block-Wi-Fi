# Block Wi-Fi on Windows

A comprehensive guide on preventing Windows 10 and Windows 11 computers from connecting to Wi-Fi networks, even when users have the correct Wi-Fi password.

---

## Overview

In shared, public, or enterprise environments, you may need to restrict Wi-Fi access completely while allowing wired Ethernet connections or completely blocking internet connectivity. This guide provides three distinct methods ranging from quick GUI toggles to robust command-line filtering and user account permission lockdowns.

---

## Method 1: Disable the Wi-Fi Adapter (Quick & Simple)

This method turns off the wireless network interface until it is manually re-enabled.

### Steps:
1. Press `Win + R` to open the **Run** dialog.
2. Type `ncpa.cpl` and press **Enter** (opens Network Connections).
3. Locate the **Wi-Fi** adapter.
4. Right-click the **Wi-Fi** adapter and select **Disable**.

> **Note:** Any user with administrative privileges can re-enable the adapter by right-clicking and selecting **Enable**. This method is not a tamper-proof restriction on its own.

---

## Method 2: Block All Wi-Fi Networks via Command Prompt (Recommended)

This method adds a system-level filter that prevents Windows from detecting or connecting to infrastructure Wi-Fi networks, even if the password is known.

### Steps:

1. **Open Command Prompt as Administrator**:
   - Press the Windows Key, type `cmd`.
   - Right-click **Command Prompt** and select **Run as administrator**.

2. **Add a Deny-All Filter**:
   Run the following command to block all infrastructure Wi-Fi networks:
   ```cmd
   netsh wlan add filter permission=denyall networktype=infrastructure
   ```

3. **Disconnect Any Active Wi-Fi Connection**:
   ```cmd
   netsh wlan disconnect
   ```

4. **Verify Active Filters**:
   Confirm that the filter has been applied:
   ```cmd
   netsh wlan show filters
   ```
   *You should see `infrastructure: Block all` listed under the active filters.*

### How to Unblock / Restore Wi-Fi Access:
When you wish to restore wireless connectivity, open Command Prompt as Administrator and run:
```cmd
netsh wlan delete filter permission=denyall networktype=infrastructure
```

---

## Method 3: Prevent Standard Users from Re-enabling Wi-Fi (Security Hardening)

If the computer is shared with other users, combine either Method 1 or Method 2 with account permission restrictions to prevent tampering:

1. **Create a Dedicated Administrator Account**:
   - Ensure your account has a strong Administrator password.
2. **Convert Other Accounts to Standard User**:
   - Go to **Settings** > **Accounts** > **Other users**.
   - Change the account type of all other users from **Administrator** to **Standard User**.
3. **Keep the Administrator Password Confidential**:
   - Standard users cannot run Command Prompt as Administrator or change adapter settings without entering the administrator password.
4. **Apply the Restrictions**:
   - Use Method 2 (WLAN filter) or Method 1 (Disable adapter) under your Administrator account.

---

## Compatibility

- Windows 10 (Home, Pro, Enterprise, Education)
- Windows 11 (Home, Pro, Enterprise, Education)

---

## License

This project is licensed under the MIT License.
