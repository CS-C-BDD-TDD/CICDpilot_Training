```bash
[johnny@localhost ~]$ ssh student7@54.89.7.155
The authenticity of host '54.89.7.155 (54.89.7.155)' can't be established.
ECDSA key fingerprint is SHA256:Ykr6geKO30gEvSLRMsaKmNGP8HOM+d1nigit/buvLPU.
ECDSA key fingerprint is MD5:a7:69:a9:3d:4f:20:d4:91:32:e3:0a:7b:26:21:f9:4a.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '54.89.7.155' (ECDSA) to the list of known hosts.
student7@54.89.7.155's password: (ansible)
[student7@ip-172-16-137-214 ~]$ ls
networking-workshop
[student7@ip-172-16-137-214 ~]$ cd networking-workshop/
[student7@ip-172-16-137-214 networking-workshop]$ ls
filter_plugins  lab_inventory  labs  networking_v2  parsers  README.md  resources  roles  templates

Usage: ansible <host-pattern> [options]

Define and run a single task 'playbook' against a set of hosts

Options:
  -a MODULE_ARGS, --args=MODULE_ARGS
                        module arguments
  --ask-vault-pass      ask for vault password
  -B SECONDS, --background=SECONDS
                        run asynchronously, failing after X seconds
                        (default=N/A)
  -C, --check           don't make any changes; instead, try to predict some
                        of the changes that may occur
  -D, --diff            when changing (small) files and templates, show the
                        differences in those files; works great with --check
  -e EXTRA_VARS, --extra-vars=EXTRA_VARS
                        set additional variables as key=value or YAML/JSON, if
                        filename prepend with @
  -f FORKS, --forks=FORKS
                        specify number of parallel processes to use
                        (default=5)
  -h, --help            show this help message and exit
  -i INVENTORY, --inventory=INVENTORY, --inventory-file=INVENTORY
                        specify inventory host path or comma separated host
                        list. --inventory-file is deprecated
  -l SUBSET, --limit=SUBSET
                        further limit selected hosts to an additional pattern
  --list-hosts          outputs a list of matching hosts; does not execute
                        anything else
  -m MODULE_NAME, --module-name=MODULE_NAME
                        module name to execute (default=command)
  -M MODULE_PATH, --module-path=MODULE_PATH
                        prepend colon-separated path(s) to module library
                        (default=[u'/home/student7/.ansible/plugins/modules',
                        u'/usr/share/ansible/plugins/modules'])
  -o, --one-line        condense output
  --playbook-dir=BASEDIR
                        Since this tool does not use playbooks, use this as a
                        subsitute playbook directory.This sets the relative
                        path for many features including roles/ group_vars/
                        etc.
  -P POLL_INTERVAL, --poll=POLL_INTERVAL
                        set the poll interval if using -B (default=15)
  --syntax-check        perform a syntax check on the playbook, but do not
                        execute it
  -t TREE, --tree=TREE  log output to this directory
  --vault-id=VAULT_IDS  the vault identity to use
  --vault-password-file=VAULT_PASSWORD_FILES
                        vault password file
  -v, --verbose         verbose mode (-vvv for more, -vvvv to enable
                        connection debugging)
  --version             show program's version number and exit

  Connection Options:
    control as whom and how to connect to hosts

    -k, --ask-pass      ask for connection password
    --private-key=PRIVATE_KEY_FILE, --key-file=PRIVATE_KEY_FILE
                        use this file to authenticate the connection
    -u REMOTE_USER, --user=REMOTE_USER
                        connect as this user (default=None)
    -c CONNECTION, --connection=CONNECTION
                        connection type to use (default=smart)
    -T TIMEOUT, --timeout=TIMEOUT
                        override the connection timeout in seconds
                        (default=60)
    --ssh-common-args=SSH_COMMON_ARGS
                        specify common arguments to pass to sftp/scp/ssh (e.g.
                        ProxyCommand)
    --sftp-extra-args=SFTP_EXTRA_ARGS
                        specify extra arguments to pass to sftp only (e.g. -f,
                        -l)
    --scp-extra-args=SCP_EXTRA_ARGS
                        specify extra arguments to pass to scp only (e.g. -l)
    --ssh-extra-args=SSH_EXTRA_ARGS
                        specify extra arguments to pass to ssh only (e.g. -R)

  Privilege Escalation Options:
    control how and which user you become as on target hosts

    -s, --sudo          run operations with sudo (nopasswd) (deprecated, use
                        become)
    -U SUDO_USER, --sudo-user=SUDO_USER
                        desired sudo user (default=root) (deprecated, use
                        become)
    -S, --su            run operations with su (deprecated, use become)
    -R SU_USER, --su-user=SU_USER
                        run operations with su as this user (default=None)
                        (deprecated, use become)
    -b, --become        run operations with become (does not imply password
                        prompting)
    --become-method=BECOME_METHOD
                        privilege escalation method to use (default=sudo),
                        valid choices: [ sudo | su | pbrun | pfexec | doas |
                        dzdo | ksu | runas | pmrun | enable | machinectl ]
    --become-user=BECOME_USER
                        run operations as this user (default=root)
    --ask-sudo-pass     ask for sudo password (deprecated, use become)
    --ask-su-pass       ask for su password (deprecated, use become)
    -K, --ask-become-pass
                        ask for privilege escalation password

Some modules do not make sense in Ad-Hoc (include, meta, etc)

[student7@ip-172-16-137-214 networking-workshop]$ ansible --version
ansible 2.6.1
  config file = /home/student7/.ansible.cfg
  configured module search path = [u'/home/student7/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/site-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.5 (default, May  3 2017, 07:55:04) [GCC 4.8.5 20150623 (Red Hat 4.8.5-14)]

[student7@ip-172-16-137-214 networking-workshop]$ cat /home/student7/.ansible.cfg
[defaults]
connection = smart
timeout = 60
inventory = /home/student7/networking-workshop/lab_inventory/hosts
host_key_checking = False
private_key_file = /home/student7/.ssh/aws-private.pem
[student7@ip-172-16-137-214 networking-workshop]$ cat /home/student7/networking-workshop/lab_inventory/hosts
[all:vars]
ansible_user=student7
ansible_ssh_pass=ansible
ansible_port=22

[routers:children]
cisco

[cisco]
rtr1 ansible_host=52.203.60.1 ansible_ssh_user=ec2-user private_ip=172.16.211.221 ansible_network_os=ios
rtr2 ansible_host=107.23.208.76 ansible_ssh_user=ec2-user private_ip=172.17.101.242 ansible_network_os=ios
rtr3 ansible_host=34.227.97.47 ansible_ssh_user=ec2-user private_ip=172.16.71.76 ansible_network_os=ios
rtr4 ansible_host=35.153.203.197 ansible_ssh_user=ec2-user private_ip=172.17.106.96 ansible_network_os=ios


[cisco:vars]
ansible_ssh_user=ec2-user
ansible_network_os=ios


[dc1]
rtr1
rtr3

[dc2]
rtr2
rtr4

[hosts]
host1 ansible_host=54.164.144.240 ansible_ssh_user=ec2-user private_ip=172.17.121.125

[control]
ansible ansible_host=54.89.7.155 ansible_ssh_user=ec2-user private_ip=172.16.137.214
[student7@ip-172-16-137-214 networking-workshop]$ rtr1 ansible_host=52.90.196.252 ansible_ssh_user=ec2-user private_ip=172.16.165.205 ansible_network_os=ios
-bash: rtr1: command not found
[student7@ip-172-16-137-214 networking-workshop]$ rtr1 ansible_host=52.90.196.252 ansible_ssh_user=ec2-user private_ip=172.16.165.205 ansible_network_os=ios
-bash: rtr1: command not found
[student7@ip-172-16-137-214 networking-workshop]$ cat /home/student7/networking-workshop/lab_inventory/hosts
[all:vars]
ansible_user=student7
ansible_ssh_pass=ansible
ansible_port=22

[routers:children]
cisco

[cisco]
rtr1 ansible_host=52.203.60.1 ansible_ssh_user=ec2-user private_ip=172.16.211.221 ansible_network_os=ios
rtr2 ansible_host=107.23.208.76 ansible_ssh_user=ec2-user private_ip=172.17.101.242 ansible_network_os=ios
rtr3 ansible_host=34.227.97.47 ansible_ssh_user=ec2-user private_ip=172.16.71.76 ansible_network_os=ios
rtr4 ansible_host=35.153.203.197 ansible_ssh_user=ec2-user private_ip=172.17.106.96 ansible_network_os=ios


[cisco:vars]
ansible_ssh_user=ec2-user
ansible_network_os=ios


[dc1]
rtr1
rtr3

[dc2]
rtr2
rtr4

[hosts]
host1 ansible_host=54.164.144.240 ansible_ssh_user=ec2-user private_ip=172.17.121.125

[control]
ansible ansible_host=54.89.7.155 ansible_ssh_user=ec2-user private_ip=172.16.137.214
[student7@ip-172-16-137-214 networking-workshop]$ vi /home/student7/networking-workshop/lab_inventory/hosts
[student7@ip-172-16-137-214 networking-workshop]$ ls
filter_plugins  lab_inventory  labs  networking_v2  parsers  README.md  resources  roles  templates
[student7@ip-172-16-137-214 networking-workshop]$ vim gather_ios_data.yml

[student7@ip-172-16-137-214 networking-workshop]$ ansible-playbook -i lab_inventory/hosts gather_ios_data.yml

PLAY [GATHER INFORMATION FROM ROUTERS] ***************************************************

TASK [GATHER ROUTER FACTS] ***************************************************************
ok: [rtr3]
ok: [rtr2]
ok: [rtr1]
ok: [rtr4]

PLAY RECAP *******************************************************************************
rtr1                       : ok=1    changed=0    unreachable=0    failed=0   
rtr2                       : ok=1    changed=0    unreachable=0    failed=0   
rtr3                       : ok=1    changed=0    unreachable=0    failed=0   
rtr4                       : ok=1    changed=0    unreachable=0    failed=0   

[student7@ip-172-16-137-214 networking-workshop]$ ansible-playbook -i lab_inventory/hosts gather_ios_data.yml -vvv
ansible-playbook 2.6.1
  config file = /home/student7/.ansible.cfg
  configured module search path = [u'/home/student7/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/site-packages/ansible
  executable location = /usr/bin/ansible-playbook
  python version = 2.7.5 (default, May  3 2017, 07:55:04) [GCC 4.8.5 20150623 (Red Hat 4.8.5-14)]
Using /home/student7/.ansible.cfg as config file
Parsed /home/student7/networking-workshop/lab_inventory/hosts inventory source with ini plugin

PLAYBOOK: gather_ios_data.yml ************************************************************
1 plays in gather_ios_data.yml

PLAY [GATHER INFORMATION FROM ROUTERS] ***************************************************
META: ran handlers

TASK [GATHER ROUTER FACTS] ***************************************************************
task path: /home/student7/networking-workshop/gather_ios_data.yml:9
<107.23.208.76> ESTABLISH LOCAL CONNECTION FOR USER: student7
<107.23.208.76> EXEC /bin/sh -c '( umask 77 && mkdir -p "` echo /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.54-52247363731034 `" && echo ansible-tmp-1532010871.54-52247363731034="` echo /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.54-52247363731034 `" ) && sleep 0'
<52.203.60.1> ESTABLISH LOCAL CONNECTION FOR USER: student7
<52.203.60.1> EXEC /bin/sh -c '( umask 77 && mkdir -p "` echo /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.57-35395052112068 `" && echo ansible-tmp-1532010871.57-35395052112068="` echo /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.57-35395052112068 `" ) && sleep 0'
<34.227.97.47> ESTABLISH LOCAL CONNECTION FOR USER: student7
<34.227.97.47> EXEC /bin/sh -c '( umask 77 && mkdir -p "` echo /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.64-199534196181801 `" && echo ansible-tmp-1532010871.64-199534196181801="` echo /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.64-199534196181801 `" ) && sleep 0'
<35.153.203.197> ESTABLISH LOCAL CONNECTION FOR USER: student7
<35.153.203.197> EXEC /bin/sh -c '( umask 77 && mkdir -p "` echo /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.69-274776989076471 `" && echo ansible-tmp-1532010871.69-274776989076471="` echo /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.69-274776989076471 `" ) && sleep 0'
Using module file /usr/lib/python2.7/site-packages/ansible/modules/network/ios/ios_facts.py
<107.23.208.76> PUT /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/tmpcNNCx4 TO /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.54-52247363731034/ios_facts.py
Using module file /usr/lib/python2.7/site-packages/ansible/modules/network/ios/ios_facts.py
<107.23.208.76> EXEC /bin/sh -c 'chmod u+x /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.54-52247363731034/ /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.54-52247363731034/ios_facts.py && sleep 0'
<52.203.60.1> PUT /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/tmpIRc8Fe TO /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.57-35395052112068/ios_facts.py
<52.203.60.1> EXEC /bin/sh -c 'chmod u+x /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.57-35395052112068/ /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.57-35395052112068/ios_facts.py && sleep 0'
Using module file /usr/lib/python2.7/site-packages/ansible/modules/network/ios/ios_facts.py
<34.227.97.47> PUT /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/tmp8o0BAV TO /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.64-199534196181801/ios_facts.py
<34.227.97.47> EXEC /bin/sh -c 'chmod u+x /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.64-199534196181801/ /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.64-199534196181801/ios_facts.py && sleep 0'
Using module file /usr/lib/python2.7/site-packages/ansible/modules/network/ios/ios_facts.py
<35.153.203.197> PUT /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/tmpriv4A5 TO /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.69-274776989076471/ios_facts.py
<35.153.203.197> EXEC /bin/sh -c 'chmod u+x /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.69-274776989076471/ /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.69-274776989076471/ios_facts.py && sleep 0'
<107.23.208.76> EXEC /bin/sh -c '/usr/bin/python /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.54-52247363731034/ios_facts.py && sleep 0'
<52.203.60.1> EXEC /bin/sh -c '/usr/bin/python /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.57-35395052112068/ios_facts.py && sleep 0'
<34.227.97.47> EXEC /bin/sh -c '/usr/bin/python /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.64-199534196181801/ios_facts.py && sleep 0'
<35.153.203.197> EXEC /bin/sh -c '/usr/bin/python /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.69-274776989076471/ios_facts.py && sleep 0'
<107.23.208.76> EXEC /bin/sh -c 'rm -f -r /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.54-52247363731034/ > /dev/null 2>&1 && sleep 0'
ok: [rtr2] => {
    "ansible_facts": {
        "ansible_net_all_ipv4_addresses": [
            "192.168.35.101", 
            "172.17.101.242", 
            "192.168.2.102", 
            "10.2.2.102", 
            "10.200.200.2", 
            "10.101.101.2"
        ], 
        "ansible_net_all_ipv6_addresses": [], 
        "ansible_net_filesystems": [
            "bootflash:"
        ], 
        "ansible_net_gather_subset": [
            "hardware", 
            "default", 
            "interfaces"
        ], 
        "ansible_net_hostname": "rtr2", 
        "ansible_net_image": "boot:packages.conf", 
        "ansible_net_interfaces": {
            "GigabitEthernet1": {
                "bandwidth": 1000000, 
                "description": null, 
                "duplex": "Full", 
                "ipv4": [
                    {
                        "address": "172.17.101.242", 
                        "subnet": "16"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "0e63.618e.9f44", 
                "mediatype": "Virtual", 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "CSR vNIC"
            }, 
            "Loopback0": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.2.102", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Loopback1": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.2.2.102", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Tunnel0": {
                "bandwidth": 100, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.101.101.2", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 9976, 
                "operstatus": "up", 
                "type": null
            }, 
            "Tunnel1": {
                "bandwidth": 100, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.200.200.2", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 9976, 
                "operstatus": "up", 
                "type": null
            }, 
            "VirtualPortGroup0": {
                "bandwidth": 750000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.35.101", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "001e.bd14.dabd", 
                "mediatype": null, 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "Virtual Port Group"
            }
        }, 
        "ansible_net_memfree_mb": 1844446, 
        "ansible_net_memtotal_mb": 2185184, 
        "ansible_net_model": "CSR1000V", 
        "ansible_net_serialnum": "9S3NEE3WFTF", 
        "ansible_net_version": "16.08.01a"
    }, 
    "changed": false, 
    "invocation": {
        "module_args": {
            "auth_pass": null, 
            "authorize": null, 
            "gather_subset": [
                "!config"
            ], 
            "host": null, 
            "password": null, 
            "port": null, 
            "provider": null, 
            "ssh_keyfile": null, 
            "timeout": null, 
            "username": null
        }
    }
}
<34.227.97.47> EXEC /bin/sh -c 'rm -f -r /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.64-199534196181801/ > /dev/null 2>&1 && sleep 0'
ok: [rtr3] => {
    "ansible_facts": {
        "ansible_net_all_ipv4_addresses": [
            "10.100.100.3", 
            "192.168.3.103", 
            "172.16.71.76", 
            "192.168.35.101", 
            "10.3.3.103"
        ], 
        "ansible_net_all_ipv6_addresses": [], 
        "ansible_net_filesystems": [
            "bootflash:"
        ], 
        "ansible_net_gather_subset": [
            "hardware", 
            "default", 
            "interfaces"
        ], 
        "ansible_net_hostname": "rtr3", 
        "ansible_net_image": "boot:packages.conf", 
        "ansible_net_interfaces": {
            "GigabitEthernet1": {
                "bandwidth": 1000000, 
                "description": null, 
                "duplex": "Full", 
                "ipv4": [
                    {
                        "address": "172.16.71.76", 
                        "subnet": "16"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "0e79.84d2.4d52", 
                "mediatype": "Virtual", 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "CSR vNIC"
            }, 
            "Loopback0": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.3.103", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Loopback1": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.3.3.103", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Tunnel0": {
                "bandwidth": 100, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.100.100.3", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 9976, 
                "operstatus": "up", 
                "type": null
            }, 
            "VirtualPortGroup0": {
                "bandwidth": 750000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.35.101", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "001e.14f6.33bd", 
                "mediatype": null, 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "Virtual Port Group"
            }
        }, 
        "ansible_net_memfree_mb": 1848904, 
        "ansible_net_memtotal_mb": 2185184, 
        "ansible_net_model": "CSR1000V", 
        "ansible_net_serialnum": "909ZZQ36YST", 
        "ansible_net_version": "16.08.01a"
    }, 
    "changed": false, 
    "invocation": {
        "module_args": {
            "auth_pass": null, 
            "authorize": null, 
            "gather_subset": [
                "!config"
            ], 
            "host": null, 
            "password": null, 
            "port": null, 
            "provider": null, 
            "ssh_keyfile": null, 
            "timeout": null, 
            "username": null
        }
    }
}
<52.203.60.1> EXEC /bin/sh -c 'rm -f -r /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.57-35395052112068/ > /dev/null 2>&1 && sleep 0'
<35.153.203.197> EXEC /bin/sh -c 'rm -f -r /home/student7/.ansible/tmp/ansible-local-31183KLC0FU/ansible-tmp-1532010871.69-274776989076471/ > /dev/null 2>&1 && sleep 0'
ok: [rtr1] => {
    "ansible_facts": {
        "ansible_net_all_ipv4_addresses": [
            "192.168.35.101", 
            "172.16.211.221", 
            "192.168.1.101", 
            "10.1.1.101", 
            "10.200.200.1", 
            "10.100.100.1", 
            "10.255.0.254"
        ], 
        "ansible_net_all_ipv6_addresses": [], 
        "ansible_net_filesystems": [
            "bootflash:"
        ], 
        "ansible_net_gather_subset": [
            "hardware", 
            "default", 
            "interfaces"
        ], 
        "ansible_net_hostname": "rtr1", 
        "ansible_net_image": "boot:packages.conf", 
        "ansible_net_interfaces": {
            "GigabitEthernet1": {
                "bandwidth": 1000000, 
                "description": null, 
                "duplex": "Full", 
                "ipv4": [
                    {
                        "address": "172.16.211.221", 
                        "subnet": "16"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "0e94.f3c8.3032", 
                "mediatype": "Virtual", 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "CSR vNIC"
            }, 
            "Loopback0": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.1.101", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Loopback1": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.1.1.101", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Tunnel0": {
                "bandwidth": 100, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.100.100.1", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 9976, 
                "operstatus": "up", 
                "type": null
            }, 
            "Tunnel1": {
                "bandwidth": 100, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.200.200.1", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 9976, 
                "operstatus": "up", 
                "type": null
            }, 
            "Tunnel2": {
                "bandwidth": 100, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.255.0.254", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 9972, 
                "operstatus": "up", 
                "type": null
            }, 
            "VirtualPortGroup0": {
                "bandwidth": 750000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.35.101", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "001e.e516.4fbd", 
                "mediatype": null, 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "Virtual Port Group"
            }
        }, 
        "ansible_net_memfree_mb": 1843920, 
        "ansible_net_memtotal_mb": 2185184, 
        "ansible_net_model": "CSR1000V", 
        "ansible_net_serialnum": "934OG5T5IJ3", 
        "ansible_net_version": "16.08.01a"
    }, 
    "changed": false, 
    "invocation": {
        "module_args": {
            "auth_pass": null, 
            "authorize": null, 
            "gather_subset": [
                "!config"
            ], 
            "host": null, 
            "password": null, 
            "port": null, 
            "provider": null, 
            "ssh_keyfile": null, 
            "timeout": null, 
            "username": null
        }
    }
}
ok: [rtr4] => {
    "ansible_facts": {
        "ansible_net_all_ipv4_addresses": [
            "10.101.101.4", 
            "192.168.4.104", 
            "172.17.106.96", 
            "192.168.35.101", 
            "10.4.4.104"
        ], 
        "ansible_net_all_ipv6_addresses": [], 
        "ansible_net_filesystems": [
            "bootflash:"
        ], 
        "ansible_net_gather_subset": [
            "hardware", 
            "default", 
            "interfaces"
        ], 
        "ansible_net_hostname": "rtr4", 
        "ansible_net_image": "boot:packages.conf", 
        "ansible_net_interfaces": {
            "GigabitEthernet1": {
                "bandwidth": 1000000, 
                "description": null, 
                "duplex": "Full", 
                "ipv4": [
                    {
                        "address": "172.17.106.96", 
                        "subnet": "16"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "0ede.14bb.1b26", 
                "mediatype": "Virtual", 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "CSR vNIC"
            }, 
            "Loopback0": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.4.104", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Loopback1": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.4.4.104", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Tunnel0": {
                "bandwidth": 100, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.101.101.4", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 9976, 
                "operstatus": "up", 
                "type": null
            }, 
            "VirtualPortGroup0": {
                "bandwidth": 750000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.35.101", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "001e.bd0c.88bd", 
                "mediatype": null, 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "Virtual Port Group"
            }
        }, 
        "ansible_net_memfree_mb": 1848686, 
        "ansible_net_memtotal_mb": 2185184, 
        "ansible_net_model": "CSR1000V", 
        "ansible_net_serialnum": "97FX68MYN58", 
        "ansible_net_version": "16.08.01a"
    }, 
    "changed": false, 
    "invocation": {
        "module_args": {
            "auth_pass": null, 
            "authorize": null, 
            "gather_subset": [
                "!config"
            ], 
            "host": null, 
            "password": null, 
            "port": null, 
            "provider": null, 
            "ssh_keyfile": null, 
            "timeout": null, 
            "username": null
        }
    }
}
META: ran handlers
META: ran handlers

PLAY RECAP *******************************************************************************
rtr1                       : ok=1    changed=0    unreachable=0    failed=0   
rtr2                       : ok=1    changed=0    unreachable=0    failed=0   
rtr3                       : ok=1    changed=0    unreachable=0    failed=0   
rtr4                       : ok=1    changed=0    unreachable=0    failed=0   

[student7@ip-172-16-137-214 networking-workshop]$ ansible-playbook -i lab_inventory/hosts gather_ios_data.yml -vvvvv
ansible-playbook 2.6.1
  config file = /home/student7/.ansible.cfg
  configured module search path = [u'/home/student7/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/site-packages/ansible
  executable location = /usr/bin/ansible-playbook
  python version = 2.7.5 (default, May  3 2017, 07:55:04) [GCC 4.8.5 20150623 (Red Hat 4.8.5-14)]
Using /home/student7/.ansible.cfg as config file
setting up inventory plugins
Parsed /home/student7/networking-workshop/lab_inventory/hosts inventory source with ini plugin
Loading callback plugin default of type stdout, v2.0 from /usr/lib/python2.7/site-packages/ansible/plugins/callback/default.pyc

PLAYBOOK: gather_ios_data.yml ************************************************************
1 plays in gather_ios_data.yml

PLAY [GATHER INFORMATION FROM ROUTERS] ***************************************************
META: ran handlers

TASK [GATHER ROUTER FACTS] ***************************************************************
task path: /home/student7/networking-workshop/gather_ios_data.yml:9
<52.203.60.1> attempting to start connection
<52.203.60.1> using connection plugin network_cli
<107.23.208.76> attempting to start connection
<107.23.208.76> using connection plugin network_cli
<34.227.97.47> attempting to start connection
<34.227.97.47> using connection plugin network_cli
<35.153.203.197> attempting to start connection
<35.153.203.197> using connection plugin network_cli
<52.203.60.1> local domain socket does not exist, starting it
<52.203.60.1> control socket path is /home/student7/.ansible/pc/800cbb5c83
<52.203.60.1> <52.203.60.1> ESTABLISH CONNECTION FOR USER: ec2-user on PORT 22 TO 52.203.60.1
<52.203.60.1> <52.203.60.1> ssh connection done, setting terminal
<52.203.60.1> <52.203.60.1> loaded terminal plugin for network_os ios
<52.203.60.1> <52.203.60.1> loaded cliconf plugin for network_os ios
<52.203.60.1> <52.203.60.1> firing event: on_open_shell()
<52.203.60.1> <52.203.60.1> ssh connection has completed successfully
<52.203.60.1> connection to remote device started successfully
<52.203.60.1> local domain socket listeners started successfully
<52.203.60.1> 
<52.203.60.1> local domain socket path is /home/student7/.ansible/pc/800cbb5c83
<52.203.60.1> ESTABLISH LOCAL CONNECTION FOR USER: student7
<52.203.60.1> EXEC /bin/sh -c '( umask 77 && mkdir -p "` echo /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010891.97-264625800947285 `" && echo ansible-tmp-1532010891.97-264625800947285="` echo /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010891.97-264625800947285 `" ) && sleep 0'
Using module_utils file /usr/lib/python2.7/site-packages/ansible/module_utils/network/__init__.py
Using module_utils file /usr/lib/python2.7/site-packages/ansible/module_utils/basic.py
Using module_utils file /usr/lib/python2.7/site-packages/ansible/module_utils/network/ios/ios.py
Using module_utils file /usr/lib/python2.7/site-packages/ansible/module_utils/network/ios/__init__.py
Using module_utils file /usr/lib/python2.7/site-packages/ansible/module_utils/six/__init__.py
Using module_utils file /usr/lib/python2.7/site-packages/ansible/module_utils/_text.py
Using module_utils file /usr/lib/python2.7/site-packages/ansible/module_utils/parsing/convert_bool.py
Using module_utils file /usr/lib/python2.7/site-packages/ansible/module_utils/parsing/__init__.py
Using module_utils file /usr/lib/python2.7/site-packages/ansible/module_utils/pycompat24.py
Using module_utils file /usr/lib/python2.7/site-packages/ansible/module_utils/connection.py
Using module_utils file /usr/lib/python2.7/site-packages/ansible/module_utils/network/common/__init__.py
Using module_utils file /usr/lib/python2.7/site-packages/ansible/module_utils/network/common/utils.py
Using module file /usr/lib/python2.7/site-packages/ansible/modules/network/ios/ios_facts.py
<52.203.60.1> PUT /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/tmpXz9Yqn TO /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010891.97-264625800947285/ios_facts.py
<52.203.60.1> EXEC /bin/sh -c 'chmod u+x /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010891.97-264625800947285/ /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010891.97-264625800947285/ios_facts.py && sleep 0'
<52.203.60.1> EXEC /bin/sh -c '/usr/bin/python /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010891.97-264625800947285/ios_facts.py && sleep 0'
<107.23.208.76> local domain socket does not exist, starting it
<107.23.208.76> control socket path is /home/student7/.ansible/pc/f812cc3fb0
<107.23.208.76> <107.23.208.76> ESTABLISH CONNECTION FOR USER: ec2-user on PORT 22 TO 107.23.208.76
<107.23.208.76> <107.23.208.76> ssh connection done, setting terminal
<107.23.208.76> <107.23.208.76> loaded terminal plugin for network_os ios
<107.23.208.76> <107.23.208.76> loaded cliconf plugin for network_os ios
<107.23.208.76> <107.23.208.76> firing event: on_open_shell()
<107.23.208.76> <107.23.208.76> ssh connection has completed successfully
<107.23.208.76> connection to remote device started successfully
<107.23.208.76> local domain socket listeners started successfully
<107.23.208.76> 
<107.23.208.76> local domain socket path is /home/student7/.ansible/pc/f812cc3fb0
<107.23.208.76> ESTABLISH LOCAL CONNECTION FOR USER: student7
<107.23.208.76> EXEC /bin/sh -c '( umask 77 && mkdir -p "` echo /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.18-261885881806978 `" && echo ansible-tmp-1532010892.18-261885881806978="` echo /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.18-261885881806978 `" ) && sleep 0'
Using module file /usr/lib/python2.7/site-packages/ansible/modules/network/ios/ios_facts.py
<107.23.208.76> PUT /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/tmpOkZz35 TO /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.18-261885881806978/ios_facts.py
<107.23.208.76> EXEC /bin/sh -c 'chmod u+x /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.18-261885881806978/ /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.18-261885881806978/ios_facts.py && sleep 0'
<107.23.208.76> EXEC /bin/sh -c '/usr/bin/python /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.18-261885881806978/ios_facts.py && sleep 0'
<35.153.203.197> local domain socket does not exist, starting it
<35.153.203.197> control socket path is /home/student7/.ansible/pc/40e1e23caf
<35.153.203.197> <35.153.203.197> ESTABLISH CONNECTION FOR USER: ec2-user on PORT 22 TO 35.153.203.197
<35.153.203.197> <35.153.203.197> ssh connection done, setting terminal
<35.153.203.197> <35.153.203.197> loaded terminal plugin for network_os ios
<35.153.203.197> <35.153.203.197> loaded cliconf plugin for network_os ios
<35.153.203.197> <35.153.203.197> firing event: on_open_shell()
<35.153.203.197> <35.153.203.197> ssh connection has completed successfully
<35.153.203.197> connection to remote device started successfully
<35.153.203.197> local domain socket listeners started successfully
<35.153.203.197> 
<35.153.203.197> local domain socket path is /home/student7/.ansible/pc/40e1e23caf
<35.153.203.197> ESTABLISH LOCAL CONNECTION FOR USER: student7
<35.153.203.197> EXEC /bin/sh -c '( umask 77 && mkdir -p "` echo /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.25-201711760336083 `" && echo ansible-tmp-1532010892.25-201711760336083="` echo /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.25-201711760336083 `" ) && sleep 0'
<34.227.97.47> local domain socket does not exist, starting it
<34.227.97.47> control socket path is /home/student7/.ansible/pc/d29a9cc65d
<34.227.97.47> <34.227.97.47> ESTABLISH CONNECTION FOR USER: ec2-user on PORT 22 TO 34.227.97.47
<34.227.97.47> <34.227.97.47> ssh connection done, setting terminal
<34.227.97.47> <34.227.97.47> loaded terminal plugin for network_os ios
<34.227.97.47> <34.227.97.47> loaded cliconf plugin for network_os ios
<34.227.97.47> <34.227.97.47> firing event: on_open_shell()
<34.227.97.47> <34.227.97.47> ssh connection has completed successfully
<34.227.97.47> connection to remote device started successfully
<34.227.97.47> local domain socket listeners started successfully
<34.227.97.47> 
<34.227.97.47> local domain socket path is /home/student7/.ansible/pc/d29a9cc65d
<34.227.97.47> ESTABLISH LOCAL CONNECTION FOR USER: student7
<34.227.97.47> EXEC /bin/sh -c '( umask 77 && mkdir -p "` echo /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.26-250768602740054 `" && echo ansible-tmp-1532010892.26-250768602740054="` echo /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.26-250768602740054 `" ) && sleep 0'
Using module file /usr/lib/python2.7/site-packages/ansible/modules/network/ios/ios_facts.py
<35.153.203.197> PUT /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/tmps5zyCY TO /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.25-201711760336083/ios_facts.py
<35.153.203.197> EXEC /bin/sh -c 'chmod u+x /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.25-201711760336083/ /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.25-201711760336083/ios_facts.py && sleep 0'
<35.153.203.197> EXEC /bin/sh -c '/usr/bin/python /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.25-201711760336083/ios_facts.py && sleep 0'
Using module file /usr/lib/python2.7/site-packages/ansible/modules/network/ios/ios_facts.py
<34.227.97.47> PUT /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/tmp359G7o TO /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.26-250768602740054/ios_facts.py
<34.227.97.47> EXEC /bin/sh -c 'chmod u+x /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.26-250768602740054/ /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.26-250768602740054/ios_facts.py && sleep 0'
<34.227.97.47> EXEC /bin/sh -c '/usr/bin/python /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.26-250768602740054/ios_facts.py && sleep 0'
<52.203.60.1> EXEC /bin/sh -c 'rm -f -r /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010891.97-264625800947285/ > /dev/null 2>&1 && sleep 0'
ok: [rtr1] => {
    "ansible_facts": {
        "ansible_net_all_ipv4_addresses": [
            "192.168.35.101", 
            "172.16.211.221", 
            "192.168.1.101", 
            "10.1.1.101", 
            "10.200.200.1", 
            "10.100.100.1", 
            "10.255.0.254"
        ], 
        "ansible_net_all_ipv6_addresses": [], 
        "ansible_net_filesystems": [
            "bootflash:"
        ], 
        "ansible_net_gather_subset": [
            "hardware", 
            "default", 
            "interfaces"
        ], 
        "ansible_net_hostname": "rtr1", 
        "ansible_net_image": "boot:packages.conf", 
        "ansible_net_interfaces": {
            "GigabitEthernet1": {
                "bandwidth": 1000000, 
                "description": null, 
                "duplex": "Full", 
                "ipv4": [
                    {
                        "address": "172.16.211.221", 
                        "subnet": "16"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "0e94.f3c8.3032", 
                "mediatype": "Virtual", 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "CSR vNIC"
            }, 
            "Loopback0": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.1.101", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Loopback1": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.1.1.101", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Tunnel0": {
                "bandwidth": 100, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.100.100.1", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 9976, 
                "operstatus": "up", 
                "type": null
            }, 
            "Tunnel1": {
                "bandwidth": 100, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.200.200.1", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 9976, 
                "operstatus": "up", 
                "type": null
            }, 
            "Tunnel2": {
                "bandwidth": 100, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.255.0.254", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 9972, 
                "operstatus": "up", 
                "type": null
            }, 
            "VirtualPortGroup0": {
                "bandwidth": 750000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.35.101", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "001e.e516.4fbd", 
                "mediatype": null, 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "Virtual Port Group"
            }
        }, 
        "ansible_net_memfree_mb": 1843920, 
        "ansible_net_memtotal_mb": 2185184, 
        "ansible_net_model": "CSR1000V", 
        "ansible_net_serialnum": "934OG5T5IJ3", 
        "ansible_net_version": "16.08.01a"
    }, 
    "changed": false, 
    "invocation": {
        "module_args": {
            "auth_pass": null, 
            "authorize": null, 
            "gather_subset": [
                "!config"
            ], 
            "host": null, 
            "password": null, 
            "port": null, 
            "provider": null, 
            "ssh_keyfile": null, 
            "timeout": null, 
            "username": null
        }
    }
}
<107.23.208.76> EXEC /bin/sh -c 'rm -f -r /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.18-261885881806978/ > /dev/null 2>&1 && sleep 0'
ok: [rtr2] => {
    "ansible_facts": {
        "ansible_net_all_ipv4_addresses": [
            "192.168.35.101", 
            "172.17.101.242", 
            "192.168.2.102", 
            "10.2.2.102", 
            "10.200.200.2", 
            "10.101.101.2"
        ], 
        "ansible_net_all_ipv6_addresses": [], 
        "ansible_net_filesystems": [
            "bootflash:"
        ], 
        "ansible_net_gather_subset": [
            "hardware", 
            "default", 
            "interfaces"
        ], 
        "ansible_net_hostname": "rtr2", 
        "ansible_net_image": "boot:packages.conf", 
        "ansible_net_interfaces": {
            "GigabitEthernet1": {
                "bandwidth": 1000000, 
                "description": null, 
                "duplex": "Full", 
                "ipv4": [
                    {
                        "address": "172.17.101.242", 
                        "subnet": "16"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "0e63.618e.9f44", 
                "mediatype": "Virtual", 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "CSR vNIC"
            }, 
            "Loopback0": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.2.102", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Loopback1": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.2.2.102", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Tunnel0": {
                "bandwidth": 100, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.101.101.2", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 9976, 
                "operstatus": "up", 
                "type": null
            }, 
            "Tunnel1": {
                "bandwidth": 100, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.200.200.2", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 9976, 
                "operstatus": "up", 
                "type": null
            }, 
            "VirtualPortGroup0": {
                "bandwidth": 750000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.35.101", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "001e.bd14.dabd", 
                "mediatype": null, 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "Virtual Port Group"
            }
        }, 
        "ansible_net_memfree_mb": 1844446, 
        "ansible_net_memtotal_mb": 2185184, 
        "ansible_net_model": "CSR1000V", 
        "ansible_net_serialnum": "9S3NEE3WFTF", 
        "ansible_net_version": "16.08.01a"
    }, 
    "changed": false, 
    "invocation": {
        "module_args": {
            "auth_pass": null, 
            "authorize": null, 
            "gather_subset": [
                "!config"
            ], 
            "host": null, 
            "password": null, 
            "port": null, 
            "provider": null, 
            "ssh_keyfile": null, 
            "timeout": null, 
            "username": null
        }
    }
}
<34.227.97.47> EXEC /bin/sh -c 'rm -f -r /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.26-250768602740054/ > /dev/null 2>&1 && sleep 0'
ok: [rtr3] => {
    "ansible_facts": {
        "ansible_net_all_ipv4_addresses": [
            "10.100.100.3", 
            "192.168.3.103", 
            "172.16.71.76", 
            "192.168.35.101", 
            "10.3.3.103"
        ], 
        "ansible_net_all_ipv6_addresses": [], 
        "ansible_net_filesystems": [
            "bootflash:"
        ], 
        "ansible_net_gather_subset": [
            "hardware", 
            "default", 
            "interfaces"
        ], 
        "ansible_net_hostname": "rtr3", 
        "ansible_net_image": "boot:packages.conf", 
        "ansible_net_interfaces": {
            "GigabitEthernet1": {
                "bandwidth": 1000000, 
                "description": null, 
                "duplex": "Full", 
                "ipv4": [
                    {
                        "address": "172.16.71.76", 
                        "subnet": "16"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "0e79.84d2.4d52", 
                "mediatype": "Virtual", 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "CSR vNIC"
            }, 
            "Loopback0": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.3.103", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Loopback1": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.3.3.103", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Tunnel0": {
                "bandwidth": 100, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.100.100.3", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 9976, 
                "operstatus": "up", 
                "type": null
            }, 
            "VirtualPortGroup0": {
                "bandwidth": 750000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.35.101", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "001e.14f6.33bd", 
                "mediatype": null, 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "Virtual Port Group"
            }
        }, 
        "ansible_net_memfree_mb": 1848904, 
        "ansible_net_memtotal_mb": 2185184, 
        "ansible_net_model": "CSR1000V", 
        "ansible_net_serialnum": "909ZZQ36YST", 
        "ansible_net_version": "16.08.01a"
    }, 
    "changed": false, 
    "invocation": {
        "module_args": {
            "auth_pass": null, 
            "authorize": null, 
            "gather_subset": [
                "!config"
            ], 
            "host": null, 
            "password": null, 
            "port": null, 
            "provider": null, 
            "ssh_keyfile": null, 
            "timeout": null, 
            "username": null
        }
    }
}
<35.153.203.197> EXEC /bin/sh -c 'rm -f -r /home/student7/.ansible/tmp/ansible-local-31321DrR4o6/ansible-tmp-1532010892.25-201711760336083/ > /dev/null 2>&1 && sleep 0'
ok: [rtr4] => {
    "ansible_facts": {
        "ansible_net_all_ipv4_addresses": [
            "10.101.101.4", 
            "192.168.4.104", 
            "172.17.106.96", 
            "192.168.35.101", 
            "10.4.4.104"
        ], 
        "ansible_net_all_ipv6_addresses": [], 
        "ansible_net_filesystems": [
            "bootflash:"
        ], 
        "ansible_net_gather_subset": [
            "hardware", 
            "default", 
            "interfaces"
        ], 
        "ansible_net_hostname": "rtr4", 
        "ansible_net_image": "boot:packages.conf", 
        "ansible_net_interfaces": {
            "GigabitEthernet1": {
                "bandwidth": 1000000, 
                "description": null, 
                "duplex": "Full", 
                "ipv4": [
                    {
                        "address": "172.17.106.96", 
                        "subnet": "16"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "0ede.14bb.1b26", 
                "mediatype": "Virtual", 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "CSR vNIC"
            }, 
            "Loopback0": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.4.104", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Loopback1": {
                "bandwidth": 8000000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.4.4.104", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 1514, 
                "operstatus": "up", 
                "type": null
            }, 
            "Tunnel0": {
                "bandwidth": 100, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "10.101.101.4", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": null, 
                "mediatype": null, 
                "mtu": 9976, 
                "operstatus": "up", 
                "type": null
            }, 
            "VirtualPortGroup0": {
                "bandwidth": 750000, 
                "description": null, 
                "duplex": null, 
                "ipv4": [
                    {
                        "address": "192.168.35.101", 
                        "subnet": "24"
                    }
                ], 
                "lineprotocol": "up ", 
                "macaddress": "001e.bd0c.88bd", 
                "mediatype": null, 
                "mtu": 1500, 
                "operstatus": "up", 
                "type": "Virtual Port Group"
            }
        }, 
        "ansible_net_memfree_mb": 1848686, 
        "ansible_net_memtotal_mb": 2185184, 
        "ansible_net_model": "CSR1000V", 
        "ansible_net_serialnum": "97FX68MYN58", 
        "ansible_net_version": "16.08.01a"
    }, 
    "changed": false, 
    "invocation": {
        "module_args": {
            "auth_pass": null, 
            "authorize": null, 
            "gather_subset": [
                "!config"
            ], 
            "host": null, 
            "password": null, 
            "port": null, 
            "provider": null, 
            "ssh_keyfile": null, 
            "timeout": null, 
            "username": null
        }
    }
}
META: ran handlers
META: ran handlers

PLAY RECAP *******************************************************************************
rtr1                       : ok=1    changed=0    unreachable=0    failed=0   
rtr2                       : ok=1    changed=0    unreachable=0    failed=0   
rtr3                       : ok=1    changed=0    unreachable=0    failed=0   
rtr4                       : ok=1    changed=0    unreachable=0    failed=0   


[student7@ip-172-16-137-214 networking-workshop]$ ansible-playbook -i lab_inventory/hosts gather_ios_data.yml -v --limit rtr1
Using /home/student7/.ansible.cfg as config file

PLAY [GATHER INFORMATION FROM ROUTERS] ***************************************************

TASK [GATHER ROUTER FACTS] ***************************************************************
ok: [rtr1] => {"ansible_facts": {"ansible_net_all_ipv4_addresses": ["192.168.35.101", "172.16.211.221", "192.168.1.101", "10.1.1.101", "10.200.200.1", "10.100.100.1", "10.255.0.254"], "ansible_net_all_ipv6_addresses": [], "ansible_net_filesystems": ["bootflash:"], "ansible_net_gather_subset": ["hardware", "default", "interfaces"], "ansible_net_hostname": "rtr1", "ansible_net_image": "boot:packages.conf", "ansible_net_interfaces": {"GigabitEthernet1": {"bandwidth": 1000000, "description": null, "duplex": "Full", "ipv4": [{"address": "172.16.211.221", "subnet": "16"}], "lineprotocol": "up ", "macaddress": "0e94.f3c8.3032", "mediatype": "Virtual", "mtu": 1500, "operstatus": "up", "type": "CSR vNIC"}, "Loopback0": {"bandwidth": 8000000, "description": null, "duplex": null, "ipv4": [{"address": "192.168.1.101", "subnet": "24"}], "lineprotocol": "up ", "macaddress": null, "mediatype": null, "mtu": 1514, "operstatus": "up", "type": null}, "Loopback1": {"bandwidth": 8000000, "description": null, "duplex": null, "ipv4": [{"address": "10.1.1.101", "subnet": "24"
```
