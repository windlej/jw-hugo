---
title: "Network Config Backup"
description: "SSH into multiple Cisco devices and pull running configs automatically. Saves timestamped backups to local disk. Built with Netmiko and designed for MSP multi-device environments."
icon: ">_"
language: "Python"
github: "https://github.com/jeremiahwindle/network-config-backup"
tags: ["python", "netmiko", "cisco", "automation", "backup"]
date: 2026-03-01
---

Pulls running configurations from multiple Cisco IOS devices over SSH and saves them as timestamped files. Reads device inventory from a YAML file — no hardcoded credentials, no hardcoded hostnames.

## What It Does

- Reads device list from `devices.yaml` (hostname, IP, credentials, device type)
- SSHs into each device using Netmiko
- Runs `show running-config` and captures output
- Saves each config as `{hostname}_{YYYY-MM-DD_HH-MM}.txt`
- Logs success/failure per device to `backup.log`
- Sends an email summary when complete (optional)

Built initially to run nightly via cron across MSP client sites. Catches config drift before it becomes a problem.

## Quick Start

```bash
pip install netmiko pyyaml
git clone https://github.com/jeremiahwindle/network-config-backup
cd network-config-backup
cp devices.example.yaml devices.yaml
# Edit devices.yaml with your inventory
python backup.py
```

## devices.yaml Format

```yaml
devices:
  - name: core-sw-01
    host: 10.0.10.1
    device_type: cisco_ios
    username: admin
    password: "{{ env_var('DEVICE_PASS') }}"

  - name: firewall-01
    host: 10.0.10.254
    device_type: cisco_asa
    username: admin
    password: "{{ env_var('DEVICE_PASS') }}"
```

Credentials are read from environment variables — no plaintext passwords in config files.
