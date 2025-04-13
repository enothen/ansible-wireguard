# ansible-wireguard
Create a Wireguard VPN between Linux hosts using Ansible

# Install and configure
Create tunnel(s) between a Wireguard server and peer(s) by adding corresponding hostnames to inventory.yml. Then run the playbook like this:
```
$ ansible-playbook setup-wireguard-vpn.yml

PLAY [Setup a Wireguard vpn using defined server and peers] *********************************************************

TASK [Gathering Facts] **********************************************************************************************
ok: [rhelpeer.sitec.net]
ok: [wgserver.sitea.net]
ok: [ubuntupeer.siteb.net]

TASK [Install and configure wireguard] ******************************************************************************

TASK [wireguard : Install packages in Debian distros] ***************************************************************
skipping: [rhelpeer.sitec.net]
included: /home/enothen/git/ansible-wireguard/roles/wireguard/tasks/install-debian.yml for wgserver.sitea.net, ubuntupeer.siteb.net

TASK [wireguard : Install Wireguard in Debian distros] **************************************************************
changed: [wgserver.sitea.net]
changed: [ubuntupeer.siteb.net]

TASK [wireguard : Install bind9] ************************************************************************************
skipping: [ubuntupeer.siteb.net]
ok: [wgserver.sitea.net]

TASK [wireguard : Install iptables] *********************************************************************************
skipping: [ubuntupeer.siteb.net]
ok: [wgserver.sitea.net]

TASK [wireguard : Install packages in Red Hat distros] **************************************************************
skipping: [wgserver.sitea.net]
skipping: [ubuntupeer.siteb.net]
included: /home/enothen/git/ansible-wireguard/roles/wireguard/tasks/install-redhat.yml for rhelpeer.sitec.net

TASK [wireguard : Install Wireguard in Red Hat distros] *************************************************************
changed: [rhelpeer.sitec.net]

TASK [wireguard : Install bind9] ************************************************************************************
skipping: [rhelpeer.sitec.net]

TASK [wireguard : Install iptables] *********************************************************************************
ok: [rhelpeer.sitec.net]

TASK [wireguard : Enable ipv4 forwarding] ***************************************************************************
skipping: [rhelpeer.sitec.net]
skipping: [ubuntupeer.siteb.net]
ok: [wgserver.sitea.net]

TASK [wireguard : Configure TCP congestion control] *****************************************************************
skipping: [rhelpeer.sitec.net]
skipping: [ubuntupeer.siteb.net]
ok: [wgserver.sitea.net]

TASK [wireguard : Configure packet buffering] ***********************************************************************
skipping: [rhelpeer.sitec.net]
skipping: [ubuntupeer.siteb.net]
ok: [wgserver.sitea.net]

TASK [wireguard : Disable ipv6] *************************************************************************************
skipping: [rhelpeer.sitec.net] => (item=net.ipv6.conf.all.disable_ipv6)
skipping: [rhelpeer.sitec.net] => (item=net.ipv6.conf.default.disable_ipv6)
skipping: [rhelpeer.sitec.net]
skipping: [ubuntupeer.siteb.net] => (item=net.ipv6.conf.all.disable_ipv6)
skipping: [ubuntupeer.siteb.net] => (item=net.ipv6.conf.default.disable_ipv6)
skipping: [ubuntupeer.siteb.net]
ok: [wgserver.sitea.net] => (item=net.ipv6.conf.all.disable_ipv6)
ok: [wgserver.sitea.net] => (item=net.ipv6.conf.default.disable_ipv6)

TASK [wireguard : Configure iptables rules] *************************************************************************
skipping: [rhelpeer.sitec.net]
skipping: [ubuntupeer.siteb.net]
included: /home/enothen/git/ansible-wireguard/roles/wireguard/tasks/configure-iptables.yml for wgserver.sitea.net

TASK [wireguard : install masquerade rule for traffic from vpn interface] *******************************************
changed: [wgserver.sitea.net]

TASK [wireguard : install rule to allow traffic from vpn port] ******************************************************
changed: [wgserver.sitea.net]

TASK [wireguard : install rule to forward traffic to wireguard interface] *******************************************
changed: [wgserver.sitea.net]

TASK [wireguard : install rule to forward traffic to wireguard interface] *******************************************
changed: [wgserver.sitea.net]

TASK [wireguard : install rule to allow traffic to vpn port] ********************************************************
changed: [wgserver.sitea.net]

TASK [wireguard : Ensure /etc/iptables exists] **********************************************************************
ok: [wgserver.sitea.net]

TASK [wireguard : Flush handlers] ***********************************************************************************

RUNNING HANDLER [wireguard : Save firewall rules] *******************************************************************
changed: [wgserver.sitea.net]

TASK [wireguard : Set fact with all possible ip addresses from VPN IP range] ****************************************
ok: [wgserver.sitea.net -> localhost]

TASK [wireguard : Check if private key exists] **********************************************************************
ok: [ubuntupeer.siteb.net]
ok: [wgserver.sitea.net]
ok: [rhelpeer.sitec.net]

TASK [wireguard : Create private key] *******************************************************************************
changed: [ubuntupeer.siteb.net]
changed: [wgserver.sitea.net]
changed: [rhelpeer.sitec.net]

TASK [wireguard : Save private key to file] *************************************************************************
changed: [ubuntupeer.siteb.net]
changed: [wgserver.sitea.net]
changed: [rhelpeer.sitec.net]

TASK [wireguard : Get content of private key] ***********************************************************************
changed: [wgserver.sitea.net]
changed: [ubuntupeer.siteb.net]
changed: [rhelpeer.sitec.net]

TASK [wireguard : Check if public key exists] ***********************************************************************
ok: [wgserver.sitea.net]
ok: [ubuntupeer.siteb.net]
ok: [rhelpeer.sitec.net]

TASK [wireguard : Create public key] ********************************************************************************
changed: [wgserver.sitea.net]
changed: [ubuntupeer.siteb.net]
changed: [rhelpeer.sitec.net]

TASK [wireguard : Save public key] **********************************************************************************
changed: [wgserver.sitea.net]
changed: [ubuntupeer.siteb.net]
changed: [rhelpeer.sitec.net]

TASK [wireguard : Get content of public key] ************************************************************************
changed: [ubuntupeer.siteb.net]
changed: [wgserver.sitea.net]
changed: [rhelpeer.sitec.net]

TASK [wireguard : Set VPN server facts] *****************************************************************************
ok: [wgserver.sitea.net]

TASK [wireguard : Create Wireguard server configuration file] *******************************************************
skipping: [rhelpeer.sitec.net]
skipping: [ubuntupeer.siteb.net]
changed: [wgserver.sitea.net]

TASK [wireguard : Add client to Wiregard server configuration] ******************************************************
skipping: [wgserver.sitea.net]
changed: [rhelpeer.sitec.net -> wgserver.sitea.net]
changed: [ubuntupeer.siteb.net -> wgserver.sitea.net]

TASK [wireguard : Create Wireguard client configuration file] *******************************************************
skipping: [wgserver.sitea.net]
changed: [ubuntupeer.siteb.net]
changed: [rhelpeer.sitec.net]

TASK [wireguard : Add ip address of Wireguard server to /etc/hosts] *************************************************
skipping: [wgserver.sitea.net]
ok: [ubuntupeer.siteb.net]
ok: [rhelpeer.sitec.net]

TASK [wireguard : Start Wireguard server] ***************************************************************************
skipping: [rhelpeer.sitec.net]
skipping: [ubuntupeer.siteb.net]
changed: [wgserver.sitea.net]

TASK [wireguard : Start Wireguard peers] ****************************************************************************
skipping: [wgserver.sitea.net]
changed: [rhelpeer.sitec.net]
changed: [ubuntupeer.siteb.net]

TASK [wireguard : Check public ip address from wireguard server] ****************************************************
skipping: [wgserver.sitea.net]
ok: [ubuntupeer.siteb.net -> wgserver.sitea.net]
ok: [rhelpeer.sitec.net -> wgserver.sitea.net]

TASK [wireguard : Check public ip address from wireguard peers] *****************************************************
skipping: [wgserver.sitea.net]
ok: [ubuntupeer.siteb.net]
ok: [rhelpeer.sitec.net]

TASK [wireguard : Display public ip addresses from server and peers] ************************************************
skipping: [wgserver.sitea.net]
ok: [rhelpeer.sitec.net] => {
    "msg": [
        "Public IPs server / peer: 1.2.3.4 / 1.2.3.4"
    ]
}
ok: [ubuntupeer.siteb.net] => {
    "msg": [
        "Public IPs server / peer: 1.2.3.4 / 1.2.3.4"
    ]
}

TASK [wireguard : Fail if ip addresses are different] ***************************************************************
skipping: [wgserver.sitea.net]
skipping: [rhelpeer.sitec.net]
skipping: [ubuntupeer.siteb.net]

PLAY RECAP **********************************************************************************************************
rhelpeer.sitec.net   : ok=19   changed=10   unreachable=0    failed=0    skipped=10   rescued=0    ignored=0
ubuntupeer.siteb.net : ok=18   changed=10   unreachable=0    failed=0    skipped=11   rescued=0    ignored=0
wgserver.sitea.net   : ok=29   changed=15   unreachable=0    failed=0    skipped=9    rescued=0    ignored=0
```

# Checking status
To recheck the public ip address that is detected for the wireguard peers run the playbook with the environment variable `task=ipcheck`:
```
$ ansible-playbook setup-wireguard-vpn.yml -e 'task=ipcheck'
```
The playbook assumes that the wireguard tunnel is up and therefore fails if a different public ip is detected between the server and each peer.

# Uninstallation
Run the playbook passing `task=uninstall` as environment variable to stop tunnels, remove configuration and packages:
```
$ ansible-playbook setup-wireguard-vpn.yml -e 'task=uninstall'
```

# Tuning
Most of the tuning included in the configuration applied by this role is based on the following article: <https://www.procustodibus.com/blog/2022/12/wireguard-performance-tuning>

# Debug info
From <https://www.wireguard.com/quickstart/>:
```
# modprobe wireguard && echo module wireguard +p > /sys/kernel/debug/dynamic_debug/control
```
