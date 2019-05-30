# ansible-intro
Introduction to Ansible

## What it Ansible

Ansible is an open-source automation platform. It can help with configuration management, application management, task automation. 

Unlike Puppet or Chef, it doesn't use an agent on the remote host, instead SSH is used. This means that you can configure almost anything you can SSH into.

No client-server configuration is needed to use it. Only requirement for the client side is Python ( since Ansible is written in Python ).

Playbooks are YAML files that express configurations, deployment, and orchestration in Ansible, and allow Ansible to perform operations on managed nodes. 

Each Playbook maps a group of hosts to a set of roles. Each role is represented by calls to Ansible tasks.

## Structure

### Best practice layout
```
├── hosts
├── playbooks
│   ├── project1-staging.yml
│   └── project1-production.yml
├── roles
│   └── project1
│       ├── files
│       │   └── project1.conf
│       ├── handlers
│       │   └── main.yml
│       ├── meta
│       │   └── main.yml
│       ├── tasks
│       │   └── main.yml
│       ├── templates
│       └── vars
│           └── main.yml
│   └── project2
│       ├── files
│       │   └── project2.conf
│       ├── handlers
│       │   └── main.yml
│       ├── meta
│       │   └── main.yml
│       ├── tasks
│       │   └── main.yml
│       ├── templates
│       └── vars
│           └── main.yml
├── vars.yml
```

## Examples

### Command line modules

#### Ping a server or group of servers
```
ansible -m ping targets

centos7 | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

#### Limit playbook run to specific server or group of servers
```
ansible-playbook playbook.yml --limit "hostname[,other-host]"
```

#### Run any shell command on remote targets
```
ansible targets -m shell -a 'whoami'

centos7 | CHANGED | rc=0 >>
root
```
```
ansible targets -m shell -a 'cat /etc/redhat-release'

centos7 | CHANGED | rc=0 >>
CentOS Linux release 7.6.1810 (Core)
```
```
ansible targets -m shell -a 'free -mlwt'

centos7 | CHANGED | rc=0 >>
              total        used        free      shared     buffers       cache   available
Mem:           1838         133        1087           8           4         612        1503
Low:           1838         750        1087
High:             0           0           0
Swap:          2047           0        2047
Total:         3886         133        3135
```
### Run this playbook
```
ansible-playbook -i hosts playbook.yaml
```