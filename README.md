linux-bridge
============

This role is used to configure linux-bridge by bridge-utils


Example Inventory
-----------------
```
vagrant1 ansible_ssh_host=10.10.10.11 ansible_ssh_port=2222 linux_bridge_bridge_name=br3 linux_bridge_device_name=enp0s8
vagrant2 ansible_ssh_host=10.10.10.12 ansible_ssh_port=2222 linux_bridge_bridge_name=br3 linux_bridge_device_name=enp0s8
```

hostvars 
--------
"linux_bridge_bridge_name" is the bridge name you want to add, "linux_bridge_device_name" is the network device name you want to attach to the new added bridge.  

If the bridge with name "linux_bridge_bridge_name" exists, this role does nothing. 

Example Playbook
----------------
```
- hosts: servers
  roles:
     - { role: frank6866.linux_bridge }

```

License
-------

MIT
