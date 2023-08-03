Keepalived (Ansible Role)
=========

Role keepalived installs keepalived and configure it

Requirements
------------

Only Debian tested

Role Variables
--------------

keepalived_config - List with <vrrp_instace> objects

### <vrrp_instance:dict>
    name - Unique name for vrrp instance
    addresses[] - identify a VRRP VIP definition block
    router_id - specify to which VRRP router id the instance belongs
    authentication - <auth_block:dict>
    members - <member_block:dict> specify individual setting for host in play

### <auth_block:dict>
type - specify which kind of authentication to use (PASS|AH)
password - specify the password string to use

### <member_block:dict>

<inventory_hostname>:
    interface<str> - specify the network interface for the instance to run on
    state<str> - specify the instance state in standard use
    priority<int> - specify the instance priority in the VRRP router

Dependencies
------------

On present moment developed and tested only for Debian 11.5

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    ---
    - name: Configure border router
    gather_facts: yes
    hosts: route-0:route-1
    roles:
        - role: keepalived
        keepalived_config:
            vrrp_instances:
            - name: VIP_0
                addresses:
                - 192.168.10.1/24
                router_id: 1
                authentication:
                type: PASS
                password: example
                members:
                route-0:
                    interface: ens36
                    state: MASTER
                    priority: 255
                route-1:
                    interface: ens36
                    state: BACKUP
                    priority: 254

License
-------

MIT

Author Information
------------------

antipov_i@hotmail.com
Ivan Antipov
github.com/TJAkalit
TG: @tjakalit
