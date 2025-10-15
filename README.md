# devopsfetch-server
devopsfetch-server


# 💻 devopsfetch

## 🚀 DevOps System Information Retrieval and Monitoring Tool

`devopsfetch` is a command-line utility designed for DevOps engineers and system administrators to quickly gather critical server health and configuration data. It provides instant, formatted snapshots of active services, applications, and user activities, along with continuous monitoring capabilities.

## ✨ Key Features

* **Ports & Services:** Display active listening ports and services.
* **Nginx Config:** List Nginx domains and their respective ports and configuration files.
* **Docker Status:** Show all Docker images and running/stopped container details.
* **User Activity:** List all user accounts and their last login times.
* **Time Range:** Query system logs (`journalctl`) within a specified time window.
* **Monitoring:** Runs continuously via a `systemd` service for historical logging.

## 📦 Installation

This tool requires **Python 3** and the `rich` library for formatted output.

1.  **Dependencies:** Ensure Python 3 and system tools are installed:

    ```bash
    sudo apt install -y python3 python3-pip net-tools lsof docker.io jq
    pip3 install rich
    ```

2.  **Deployment:** Place the script and set permissions:

    ```bash
    sudo cp devopsfetch.py /usr/local/bin/devopsfetch
    sudo chmod +x /usr/local/bin/devopsfetch
    ```

3.  **Monitoring Setup:** (Requires the provided `devopsfetch.service` file setup)

    ```bash
    sudo systemctl daemon-reload
    sudo systemctl enable --now devopsfetch.service
    ```

## 💡 Usage

Run the tool using the executable name (`devopsfetch`) followed by a flag. Use the help flag for a full reference.

```bash
# Get help
devopsfetch -h

# 1. Check all active ports
devopsfetch -p

# 2. Get details for a specific port (e.g., SSH)
devopsfetch -p 22

# 3. List all Docker images and containers
devopsfetch -d

# 4. View configuration for a specific Nginx domain
devopsfetch -n example.com

# 5. Show user 'admin' details and recent logins
devopsfetch -u admin

# 6. View logs from 8 AM to 9 AM today
devopsfetch -t "2025-10-16 08:00:00" "2025-10-16 09:00:00"


/var/log/devopsfetch.log

sudo tail -f /var/log/devopsfetch.log
