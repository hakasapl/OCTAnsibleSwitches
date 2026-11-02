# OCTAnsibleSwitches

Switch manifests for the Open-Cloud Testbed @ MGHPCC

Ansible site for OCT switches, uses [cci_moc.stateful_switches](https://galaxy.ansible.com/ui/repo/published/cci_moc/stateful_switches/) for stateful configuration. This repository holds the inventory and the switch
manifests. MOC switches are managed separately in [ansible-switches](https://github.com/hakasapl/ansible-switches).

## Site Setup

1. Install newest version of ansible
1. Install required PyPI packages:
    1. `pip install --user ansible-pylibssh`
1. Install the required ansible collections: `ansible-galaxy collection install -r requirements.yaml`

Switch credentials are read from the `ANSIBLESW_OCT_USER` and `ANSIBLESW_OCT_PASS`
environment variables.

## Configuration

The VLAN manifest is in `group_vars/all/vlans.yaml`, and the interface manifest of each
switch is in `host_vars/<switch>/interfaces.yaml`. The fields, and which switch OSes
support each of them, are listed in the
[collection README](https://github.com/CCI-MOC/ansible-stateful-switches#manifest-fields).

Every switch is in the `oct` inventory group, so every VLAN in the manifest needs
`oct` in its `fabrics` to be configured.

## OCT Specific Documentation

### Naming Convention

Network equipment addresses follow a common convention. Each list item represents one octet of an IPv4 address:

* `10.`
* `81` for OCT (`80` is MOC/NERC)
* `[1,2]` 1 for core networking, 2 for rack networking
* `10*<rack number> + unit number` Each rack gets its own unique number. For example, 3 switches in a rack might be `21`, `22`, and `23`
