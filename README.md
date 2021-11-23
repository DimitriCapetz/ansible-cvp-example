# ansible-cvp-example

# Ansible & CVP Integration Framework

This repo focuses on the basic interactions between CVP and Ansible using the Arista AVD/CVP Collections.  It allows the user flexibility in managing device configurations with CVP and Ansible.  Configlets make up a device's full configuration.  You can manage the configlets inside of CVP or generate them dynamically with Ansible and merge them inside of CVP.

## Requirements

- Python 3 & Ansible 2.9+
- Clone Arista AVD and CVP collections (instructions below)
- Update `ansible.cfg` with collections_path (already done in this repository)

## Clone Arista AVD & CVP Collections

```bash
# Create a directory for collections
mkdir collections
cd collections

# Clone Arista AVD & CVP collections
git clone https://github.com/aristanetworks/ansible-avd.git
git clone https://github.com/aristanetworks/ansible-cvp.git

```

Update `ansible.cfg` with the path to the Arista AVD & CVP collections

```bash
[defaults]
collections_paths = /collections/ansible-cvp:/collections/ansible-avd/
```

## Data Inputs

There are a few files that need to be updated to provide data input for the playbooks.

- `inventory.yml` - Update CVP host with ip or fqdn of your CVP system

- `group_vars/CVP_SERVERS/authconnection.yml` - CVP login and password and connection info
- `group_vars/CVP_SERVERS/containers.yml` - Dictionary of Container Topology
- `group_vars/CVP_SERVERS/devices.yml` - Dictionary of Devices, Containers, Configlets

## Playbooks

- `playbooks/update_cvp.yml` - Updates Continer Topology & Uploads configlets into CVP and attaches them to the appropriate device and/or container.

### Running playbooks

```bash
# Update Device configlets and Container Location
ansible-playbook playbooks/update_cvp.yml --tags device
```
