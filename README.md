# Nutanix Role to configure VM HA for AHV in Prism Element

This Ansible role sets the VM HA configuration for a cluster running AHV via Prism Element.


## Role Variables

| Variable                       | Required | Default  | Choices                                                                         | Comments                                                                                                                                                                                                                          |
|--------------------------------|----------|----------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| nutanix_host                   | yes      |         |                                                                                 | The IP address or FQDN for the Prism (Element only) to which you want to connect.                                                                                                                                                  |
| nutanix_username               | yes      |         |                                                                                 | A valid username with appropriate rights to access the Nutanix API.                                                                                                                                                                |
| nutanix_password               | yes      |         |                                                                                 | A valid password for the supplied username.                                                                                                                                                                                        |
| nutanix_port                   | no       | 9440    |                                                                                 | The Prism TCP port.                                                                                                                                                                                                                |
| validate_certs                 | no       | no      | yes / no                                                                        | Whether to check if Prism UI certificates are valid.                                                                                                                                                                               |
| nutanix_prism_desired_ha_state | no       | no       |                                                                                 | Whether to check if Prism UI certificates are valid.                                                                                                                                                                              |
| prism_desired_ha_state         | yes      |          | ['BestEffort', 'HighlyAvailable']                                               | The target HA state. BestEffort has no reservation and will restart VMs as long as there is sufficient capacity. HighlyAvailable reserves capacity for all powered on VMs and therefore guarantees capacity to power VMs back on. |


## Dependencies

- grdavies.nutanix_role_prism_init_api


## Example Playbook

This playbook will set the VM HA state to highly available (ie. VM reservation).
```
- hosts: localhost
  gather_facts: false
  roles:
    - role: grdavies.nutanix_role_prism_ha
  vars:
    nutanix_host: 10.38.185.37
    nutanix_username: admin
    nutanix_password: nx2Tech165!
    prism_desired_ha_state: HighlyAvailable
```

This playbook will set the VM HA state to best effort.
```
- hosts: localhost
  gather_facts: false
  roles:
    - role: grdavies.nutanix_role_prism_ha
  vars:
    nutanix_host: 10.38.185.37
    nutanix_username: admin
    nutanix_password: nx2Tech165!
    prism_desired_ha_state: BestEffort
```


## License

See LICENSE.md

## Author Information

Ross Davies
