# Home Lab Automation: Network and Media Suite

This repository contains a modular Ansible automation stack designed to manage a hybrid home lab environment consisting of Ubiquiti networking gear, Ubuntu-based media services, and Synology storage.

This was created to help me manage updating my homelab setup that I had been doing manually up until this point.

## Architecture Overview
The project is structured to handle diverse hardware constraints, specifically managing devices that lack Python interpreters (EdgeRouter and UAP) alongside full Linux servers.

* Networking: Ubiquiti EdgeRouter X and UAP-AC-Lite (Python-less management)
* Controller: Ubuntu Server (Network Controller)
* Media: Ubuntu Server running Emby and Tailscale
* Storage: Synology NAS (Managed via API)

## Project Structure
.
├── main_playbook.yaml       # Master orchestrator
├── inventory.ini            # Device inventory and connection vars
├── group_vars/
│   └── all/
│       └── vault.yaml       # Encrypted secrets (Excluded from Git)
└── plays/
    ├── network_check.yaml   # Firmware version auditing
    ├── network_controller.yaml # Controller OS updates
    ├── media_server.yaml    # Linux patching and service health
    ├── network_hardware.yaml # Ubiquiti firmware deployment
    └── synology_nas.yaml    # Storage API checks

## Usage

### Prerequisites
1. Install Ansible in WSL: sudo apt install ansible

### Running a Check (Dry Run)
ansible-playbook main_playbook.yaml --check

### Executing Full Maintenance
ansible-playbook main_playbook.yaml

## Security Note
Sensitive data including SSH credentials, sudo passwords, and API keys are encrypted via Ansible Vault. An inventory.example and vault.example are provided for reference on required variables.