# V2Ray Playbook

This playbook deploys v2ray+ws+tls+nginx.

- NGINX installation
- V2Ray installation
- Certificate handling
- HTTPS + WebSocket setup

Requirements
------------

**Ansible**

This playbook was developed and tested with [maintained](https://docs.ansible.com/ansible/latest/reference_appendices/release_and_maintenance.html#release-status) versions of Ansible. Backwards compatibility is not guaranteed.

Instructions on how to install Ansible can be found in the [Ansible website](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html).

Platforms
---------
Tested OK on Ubuntu 18.04


**Ansible NGINX Role**

This role installs NGINX Open Source. Instructions on how to install it can be found in the [Ansible NGINX Role website](https://github.com/nginxinc/ansible-role-nginx).

## Usage

- Prepare hostname for the server to deploy V2Ray
- Add hostname or IP address to inventory
```INI
[all]
example.com

[all:vars]
ansible_connection=ssh
ansible_user=root
```
- Make sure you have setup ssh connection properly
- Start to deployment with below cmd
```BASH
ansible-playbook -i inventory main.yml --limit do -e "v2ray_domain=[example.com]"

Output:
...
TASK [v2ray : Show config info]
ok: [example.com] => {
    "msg": [
        "v2ray id: 58f9a8cb-876c-5359-b24d-3e456ef68d0b",
        "v2ray ws path: /cBbbAFjawOdFQas"
    ]
}

```

- Checking if https is working, if https is't workding, this might be a known issue of Ansible, sometimes file module doesn't work as expected. You should try below cmd.
```BASH
ansible-playbook -i inventory main.yml --limit do -e "v2ray_domain=[example.com]" -t redo
```
- Checking if V2Ray is working, below is necessary keys for client
```
address:  example.com
port:     443
id:       58f9a8cb-876c-5359-b24d-3e456ef68d0b
alterId:  64
security: auto
netowrk:  ws
path:     /cBbbAFjawOdFQas
tls:      enabled
```

## License
[MIT](https://choosealicense.com/licenses/mit/)
