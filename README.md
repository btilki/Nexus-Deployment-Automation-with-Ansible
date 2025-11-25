# Nexus Deployment Automation with Ansible

Automate the installation and setup of a Sonatype Nexus repository server using Ansible.

## Project Overview

This repository contains Ansible automation scripts to install and configure Sonatype Nexus, a repository manager for binaries, artifacts, and docker images. The automation includes all necessary steps from preparing the server environment, downloading and unpacking Nexus, setting up system users and permissions, starting Nexus as a service, and verifying its status.

## Key Files

- [`deploy-nexus.yaml`](https://github.com/btilki/Nexus-Deployment-Automation-with-Ansible/blob/main/deploy-nexus.yaml): Main Ansible playbook for Nexus installation and configuration.
- [`hosts`](https://github.com/btilki/Nexus-Deployment-Automation-with-Ansible/blob/main/hosts): Example inventory file.
- [`ansible.cfg`](https://github.com/btilki/Nexus-Deployment-Automation-with-Ansible/blob/main/ansible.cfg): Ansible configuration.
- [`nexus.sh`](https://github.com/btilki/Nexus-Deployment-Automation-with-Ansible/blob/main/nexus.sh): Helper shell script (if included in your workflow).

## Playbook: `deploy-nexus.yaml`

This playbook automates the following steps:

1. **Install Dependencies**  
   - Updates apt package cache.
   - Installs Java 8 (required for Nexus) and net-tools.

2. **Download and Extract Nexus**  
   - Downloads the latest Nexus installer from Sonatype.
   - Extracts Nexus to `/opt/nexus` if not already present.

3. **Create Nexus User and Permissions**  
   - Ensures `nexus` Unix group and user exists.
   - Assigns ownership of `/opt/nexus` and `/opt/sonatype-work` to the new user/group.

4. **Configure and Start Nexus**  
   - Sets `run_as_user="nexus"` in Nexus configuration.
   - Starts the Nexus service using the Nexus user.

5. **Verification**  
   - Checks with `ps` and `netstat` to verify Nexus is running.
   - Includes a pause to allow startup.

## Requirements

- Ansible installed on your control machine.
- A target host (inventory group `nexus_server`) with Ubuntu/Debian OS.
- Root SSH access to the target server.

## Usage

1. **Update Inventory**  
   Edit the `hosts` file to add your target server(s) under the `nexus_server` group.

2. **Configure Ansible (Optional)**  
   Edit `ansible.cfg` for custom Ansible settings.

3. **Run the Playbook**

   ```sh
   ansible-playbook -i hosts deploy-nexus.yaml
   ```

## Customization

- You can modify the playbook to use a specific Nexus version by updating the download URL.
- The default installation path is `/opt/nexus` and workspace at `/opt/sonatype-work`.

## License

MIT

## References

- [Sonatype Nexus Documentation](https://help.sonatype.com/)
