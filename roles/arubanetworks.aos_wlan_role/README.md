
aos-wlan-ansible-role
=====================

This Ansible Network role provides a set of platform dependent configuration management modules specifically designed for the ArubaOS (AOS) Mobility Master and Standalone Controllers.

Requirements
------------

* Python 2.7 or 3.5+
* Ansible 2.8.1 or later  
* Minimum supported AOS firmware version 8.0

Installation
------------

Through Github, use the following command. Use option `-f` to overwrite current role version:

```
ansible-galaxy install git+https://github.com/aruba/aos-wlan-ansible-role.git
```

Through Galaxy:

```
ansible-galaxy install arubanetworks.aos_wlan_role
```

Inventory Variables
--------------

The variables that should be defined in your inventory for your AOS host are:

* `ansible_host`: IP address of controller in `A.B.C.D` format  
* `ansible_user`: Username for controller in `plaintext` format  
* `ansible_password`: Password for controller in `plaintext` format  
* `ansible_connection`: Must always be set to `httpapi`  
* `ansible_network_os`: Must always be set to `aos`
* `ansible_httpapi_port`: Must always be set to `4343`
* `ansible_httpapi_use_ssl`: Set `True` as AOS uses port 4343 for REST  
* `ansible_httpapi_validate_certs`: Set `True` or `False` depending on if Ansible should attempt to validate      certificates

### Sample Inventories:

Sample `inventory.yml`:

```yaml
all:
  hosts:
    controller:
      ansible_host: 10.1.1.1
      ansible_user: admin
      ansible_password: password
      ansible_connection: httpapi
      ansible_network_os: aos
      ansible_httpapi_port: 4343
      ansible_httpapi_validate_certs: True
      ansible_httpapi_use_ssl: True
```

Sample `inventory.ini`:

```ini
aos_1 ansible_host=10.1.1.1 ansible_user=admin ansible_password=password ansible_connection=httpapi ansible_network_os=aos ansible_httpapi_port=4343 ansible_httpapi_validate_certs=True ansible_httpapi_use_ssl=True
```

Example Playbook
----------------

If role installed through [Github](https://github.com/aruba/aos-wlan-ansible-role)
set role to `aos-wlan-ansible-role`:

```yaml
    ---
    -  hosts: all
       roles:
        - role: aos-wlan-ansible-role
       tasks:
         - name: Create a radius server
           aos_api_config:
             method: POST
             config_path: /md/SLR
             data:
              - rad_server:
                  - rad_server_name: test-dot1x
                    rad_host:
                      host: 1.1.1.1
```

If role installed through [Galaxy](https://galaxy.ansible.com/arubanetworks/aos8_role)
set role to `arubanetworks.aos_wlan_role`:

```yaml
    ---
    -  hosts: all
       roles:
        - role: arubanetworks.aos_wlan_role
       tasks:
         - name: Create a radius server
           aos_api_config:
             method: POST
             config_path: /md/SLR
             data:
              - rad_server:
                  - rad_server_name: test-dot1x
                    rad_host:
                      host: 1.1.1.1
```

You can also find pre-written playbooks for reference in the **sample_playbooks** directory on the GitHub repository. There are multiple playbooks for various use-cases/tasks typically performed on the Mobility Master, using different modules available with this role. You can choose an intended playbook and use it to build your own playbooks. 

Contribution
-------
At Aruba Networks we're dedicated to ensuring the quality of our products, if you find any
issues at all please open an issue on our [Github](https://github.com/aruba/aos-wlan-ansible-role) and we'll be sure to respond promptly!


License
-------

Apache 2.0

Author Information
------------------
Jay Pathak (jayp193)  
Karthikeyan Dhandapani (kdhandapani)  
