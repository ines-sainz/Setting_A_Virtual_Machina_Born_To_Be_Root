# Setting A Virtual Machine Born2beRoot

## Overview
The Born2beRoot project is designed to introduce system administration and virtualization by setting up a secure and well-configured Linux server inside a virtual machine. The main objective is to follow strict system configuration guidelines while ensuring security best practices are implemented. This project was completed using **Debian**.

## Setting Up the Virtual Machine
I created a virtual machine using **VirtualBox**. The system was installed with **Debian**, ensuring that only the necessary packages were included, avoiding any graphical interface (X.org or similar). This ensures a minimal setup, making the system lightweight and secure.

### Partitioning and Disk Setup
A key part of the project was configuring **LVM (Logical Volume Manager)** and setting up at least **two encrypted partitions**. This ensures better disk management and adds security by encrypting sensitive data.

### User and Group Management
- Created a **root** user and a separate user with my name `ines`.
- Configured **strict password policies** to enforce security:
  - Password expiration every **30 days**.
  - Minimum **2 days** before allowing a password change.
  - Users receive a warning **7 days** before password expiration.
  - Password must be **at least 10 characters long**, containing an uppercase letter, a lowercase letter, and a number.
  - Cannot contain the username and should not repeat characters more than **3 times in a row**.
  - For non-root users, at least **7 new characters** must be different from the old password.

### Sudo Configuration
- Installed and configured **sudo** with strict policies:
  - Limited authentication attempts to **3**.
  - Display a **custom error message** when incorrect credentials are entered.
  - Log every sudo command execution to **/var/log/sudo/**.
  - Restricted `PATH` to **secure directories** only.
  - **TTY mode enabled** for added security.

## Network and Security Configuration
### SSH Server
- Configured SSH to run on **port 4242** instead of the default 22.
- Disabled root login via SSH to enhance security.
- Ensured SSH access was properly set up for a new user created during testing.

### Firewall (UFW)
- Installed and configured **UFW (Uncomplicated Firewall)**.
- Allowed **only port 4242** (for SSH) and blocked all other external connections.
- Ensured the firewall is **enabled at boot** to maintain security.

### SELinux / AppArmor
- Since I used **Debian**, I enabled **AppArmor** at startup.
- Configured AppArmor to enforce strict security rules for system processes.

## Monitoring Script (monitoring.sh)
I developed a **Bash script** that runs automatically every **10 minutes**, displaying system statistics using the `wall` command. The script provides:
- **System architecture and kernel version**.
- **Number of physical and virtual CPU cores**.
- **RAM usage and disk usage (in percentage)**.
- **Current CPU load**.
- **Last system reboot time**.
- **LVM status** (active or not).
- **Number of active SSH connections**.
- **Logged-in users count**.
- **Network information** (IP address and MAC address).
- **Number of sudo commands executed**.

The script was designed to be **error-free** and ensure all required information is displayed in a readable format.

## Additional Configurations
- Configured the **hostname**.
- Ensured that the system has a **strong password policy** applied globally.
- Created an additional user and assigned them to group `sudo`.
- Restricted access to **only necessary directories** for security reasons.

## Bonus Features Implemented
To further extend the project, I implemented additional features:
- **Proper disk partitioning**, following best practices for security and efficiency.
- **Set up a WordPress website**, running on:
  - **Lighttpd** as a lightweight web server.
  - **MariaDB** for database management.
  - **PHP** for dynamic content.
- **Installed and configured an additional service** `LitteSpeed` that enhances the system.

## Summary
This project provided hands-on experience in Linux system administration, security configurations, and virtualization. I successfully set up a **fully functional and secure Debian server** while following all the required guidelines. The system is designed to be **secure, efficient, and easy to maintain**, with automated monitoring in place.
