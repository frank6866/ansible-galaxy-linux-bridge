linux-bridge
============

This role installs and configures linux-bridge.


hostvars 
--------
"linux_bridge_bridge_name" is the bridge name you want to add, "linux_bridge_device_name" is the network device name you want to attach to the new added bridge.  

If the bridge with name "linux_bridge_bridge_name" exists, this role does nothing. 

Example Playbook
----------------

Inventory file:

```

vagrant1 linux_bridge_bridge_name=br3 linux_bridge_device_name=enp0s8
vagrant2 linux_bridge_bridge_name=br3 linux_bridge_device_name=enp0s8

```

Playbook:

```

- hosts: servers
  roles:
     - { role: frank6866.linux_bridge }

```


License
-------

MIT
