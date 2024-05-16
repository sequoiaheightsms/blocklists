# Honeypot Blocklists from Sequoia Heights MS

## Overview

This repository provides free blocklists compiled from our honeypot network. It contains IP addresses that have attempted unauthorized access, serving as a valuable resource for enhancing network security.

## Features

- Regularly updated list of malicious IP addresses.
- Easy integration with various firewalls and security systems.
- Helps prevent unauthorized access and potential security breaches.

## Products

This repository offers two separate products:

1. **Honeypot Blocklist Probe**: Collects IPs from Fail2ban and uploads them to GitHub.
2. **Honeypot Blocklist Client**: Syncs IPs from GitHub and applies them to Firewalld.

## Installation

### Prerequisites

Ensure you have the following dependencies installed:

- `gcc`
- `systemd`
- `fail2ban` (for the probe)
- `logrotate`

### Installing from RPMs (x86_64)

1. **Download the RPM files**

   Download the latest RPMs for the probe and client from the [releases page](https://github.com/sequoiaheightsms/honeypot-blocklist/releases).

2. **Install the Probe**

   ```bash
   sudo yum install honeypot-blocklist-probe-<version>.el9.x86_64.rpm
   ```

3. **Install the Client**

   ```bash
   sudo yum install honeypot-blocklist-client-<version>.el9.x86_64.rpm
   ```

### Cloning the Repository

```bash
git clone https://github.com/sequoiaheightsms/honeypot-blocklist.git
```

## Configuration

### Honeypot Blocklist Probe

The probe will generate an SSH key pair (if it doesn't already exist) for secure communication with GitHub. The key will be labeled as `id_rsa_probe`. If the key exists, it will not generate a new one.

After installation, configure Fail2ban by editing but probe defaults are following `/etc/fail2ban/jail.local`:

```ini
[sshd]
enabled  = true
port     = ssh
logpath  = %(sshd_log)s
backend  = %(sshd_backend)s
maxretry = 2
bantime  = 2h
```

### Honeypot Blocklist Client

The client syncs the blocklist from GitHub and applies the IPs to Firewalld.

## Logging

Both the probe and client log their activities to:

- Probe: `/var/log/honeypot-probe.log`
- Client: `/var/log/honeypot-client.log`

Log rotation is handled by `logrotate` with the following configurations:

- Probe: `/etc/logrotate.d/honeypot-probe`
- Client: `/etc/logrotate.d/honeypot-client`

## Contributing

We welcome contributions from the community. Here’s how you can contribute without using the honeypot probe:

1. **Fork the Repository**: Click on the "Fork" button on the top right of this page.
2. **Clone Your Fork**: Clone your forked repository to your local machine.

   ```bash
   git clone https://github.com/yourusername/honeypot-blocklist.git
   ```

3. **Create a Branch**: Create a new branch for your feature or bugfix.

   ```bash
   git checkout -b feature-name
   ```

4. **Make Your Changes**: Make your changes to the code.
5. **Commit Your Changes**: Commit your changes with a descriptive commit message.

   ```bash
   git commit -m "Description of changes"
   ```

6. **Push Your Changes**: Push your changes to your fork.

   ```bash
   git push origin feature-name
   ```

7. **Create a Pull Request**: Create a pull request from your forked repository on GitHub.

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Contact

Please contact [Robert Romero](mailto:robert.romero@sequoiaheightsms.com).

## Acknowledgments

We want to thank all contributors and the community for their support and contributions.


