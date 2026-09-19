# Samba File Server on Ubuntu Linux

A beginner-friendly Linux administration project demonstrating how to configure a **Samba file server on Ubuntu Linux** and access a shared directory from a **Windows client** over a local network.

## Project Overview

In this project, I configured Samba to:

* Install and verify the Samba service
* Create a shared directory
* Create a Samba user
* Configure `smb.conf`
* Validate the Samba configuration
* Configure firewall access
* Create and test files in the shared directory
* Access the Linux share from Windows

## Environment

| Component    | Details            |
| ------------ | ------------------ |
| Server OS    | Ubuntu Linux       |
| Client OS    | Windows 10/11      |
| File Sharing | Samba (SMB/CIFS)   |
| Server IP    | `192.168.0.104`    |
| Share Name   | `samba_share`      |
| Share Path   | `/opt/samba-share` |

> The IP address may be different depending on the local network.

---

## Project Structure

```text
samba-file-server-ubuntu/
│
├── config/
│   └── smb.conf.example
│
├── screenshots/
│   ├── 01-samba-installation-and-status.png
│   ├── 02-create-share-directory-and-user.png
│   ├── 03-backup-smb-conf-and-testparm.png
│   ├── 04-smb-conf-overview.png
│   ├── 05-samba-share-configuration.png
│   ├── 06-firewall-samba-rule.png
│   ├── 07-create-test-files.png
│   ├── 08-server-ip-verification.png
│   ├── 09-windows-network-share-path.jpg
│   └── 10-windows-share-access.jpg
│
├── .gitignore
├── LICENSE
└── README.md
```

---

# Setup and Configuration

## 1. Install Samba

Update the package repository and install Samba.

```bash
sudo apt update
sudo apt install samba -y
```

Check the Samba service:

```bash
sudo systemctl status smbd
```

Enable Samba to start automatically:

```bash
sudo systemctl enable smbd
```

---

## 2. Create the Shared Directory

Create the directory that will be shared with Windows.

```bash
sudo mkdir -p /opt/samba-share
```

Check the directory:

```bash
ls -ld /opt/samba-share
```

---

## 3. Create a Samba User

Create a Linux user:

```bash
sudo useradd samba-user
```

Set a Samba password:

```bash
sudo smbpasswd -a samba-user
```

The Samba password is used when connecting to the share from Windows.

---

## 4. Configure Samba

Create a backup of the original configuration file:

```bash
sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.backup
```

Edit the Samba configuration:

```bash
sudo nano /etc/samba/smb.conf
```

Add the following share configuration:

```ini
[samba_share]
   path = /opt/samba-share
   browseable = yes
   read only = no
```

Save the file.

---

## 5. Test the Samba Configuration

Check the configuration for errors:

```bash
testparm
```

If the configuration is valid, Samba will display the loaded configuration without critical errors.

---

## 6. Configure Firewall

If `ufw` is enabled on Ubuntu, allow Samba traffic:

```bash
sudo ufw allow samba
```

Check the firewall status:

```bash
sudo ufw status
```

If `ufw` is not being used, firewall configuration may depend on the Linux environment.

---

## 7. Restart Samba

Apply the configuration:

```bash
sudo systemctl restart smbd
```

Verify the service:

```bash
sudo systemctl status smbd
```

---

## 8. Create Test Files

Create a test directory:

```bash
sudo mkdir -p /opt/samba-share/MyDocuments
```

Create sample files:

```bash
sudo touch /opt/samba-share/MyDocuments/test-file.txt
sudo touch /opt/samba-share/MyDocuments/sample-document.txt
```

Check the files:

```bash
ls -l /opt/samba-share/MyDocuments/
```

---

## 9. Check the Server IP Address

Find the server IP address:

```bash
ip addr
```

Example:

```text
192.168.0.104
```

The actual IP address can be different depending on the network.

---

# Windows Client Access

On the Windows computer:

1. Press **Win + R**
2. Enter the Samba network path:

```text
\\192.168.0.104\samba_share
```

3. Press **Enter**
4. Enter the Samba username and password
5. Open `MyDocuments`
6. Verify the test files

The shared files should now be accessible from Windows.

---

# Screenshots

| No. | Description                               |
| --- | ----------------------------------------- |
| 01  | Samba installation and service status     |
| 02  | Shared directory and Samba user creation  |
| 03  | Samba configuration backup and `testparm` |
| 04  | Samba configuration file overview         |
| 05  | Samba share configuration                 |
| 06  | Firewall Samba rule                       |
| 07  | Test file creation                        |
| 08  | Server IP verification                    |
| 09  | Windows network share path                |
| 10  | Samba files accessed from Windows         |

---

# Key Skills Practiced

* Linux package management
* Linux user management
* Samba installation and configuration
* File and directory management
* Linux service management with `systemctl`
* Samba authentication
* Basic firewall configuration
* Network troubleshooting
* Linux-to-Windows file sharing
* Configuration validation using `testparm`

---

# What I Learned

This project helped me understand how a Linux server can provide file-sharing services to Windows clients using the **SMB/CIFS protocol**.

I also practiced basic Linux administration tasks such as service management, user creation, configuration files, firewall rules, and network connectivity testing.

---

## Author

**Mahesh Arde**

BCA Computer Science Student

GitHub: [MaheshArde2002](https://github.com/MaheshArde2002)
