ansible-keepalived: Ansible role for setting up keepalived 
============================================================
This role sets up keepalived for an standard setup of:
  - One virtual IP
  - several hosts

You just need to provide an small amount of information to have it running
  - Add "keepalived" role to the hosts
  - Add variable keepalived_daemon_checked: "process or daemon" to check
  - Add variable keepalived_shared_ip: "floating IP address" 

Other variables can be configured, overwriting defaults/main.yml

Keepalived watch process to influence on which node should be the master. Setting
variable "keepalived_check_process" to the name of the process will do. I use keepalived
to give high availability to haproxy, so I use.

keepalived_check_process: "haproxy"

The master is the host with the last octet greatest than others.
For example, if have 5 hosts with IP from 192.168.1.1 to 192.168.1.5,
the master will be the host with IP 192.168.1.5.

Dependencies
------------
Works with Debian/Ubuntu

Role Variables
--------------
	keepalived_auth_pass: "1111"
	keepalived_router_id: "52"
	keepalived_shared_iface: "eth0"
	keepalived_shared_ip: "192.168.1.200"
	keepalived_check_process: "keepalived"
	keepalived_priority: "100"
	keepalived_backup_priority: "50"

Example Playbook
-------------------------

    - hosts: 
      - s1
      - s2
      roles:
         - { role: keepalived, keepalived_shared_ip: "192.168.1.1", keepalived_daemon_checked: "dockerd" }


Testing & trying
------------------


License
-------
Apache

Author Information
------------------
Fabrizio2210, forked by 
Toni Comerma - tcomerma (at) gmail.com
Collaborator Information
------------------------

Pablo Estigarribia - pablodav (at) gmail dot com
