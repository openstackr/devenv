# Environment Setup

> Most of these will move into Vagrant and get automated

## Create servers

    vagrant up

## Login to servers

    vagrant ssh salt
    vagrant ssh server1
    vagrant ssh server2


## Optional: Install emacs

    [root@salt ~]# yum install emacs -y
    [root@server1 ]# yum install emacs -y
    [root@server2 ]# yum install emacs -y

## Clean firewall rules on Master

    [root@salt ~]# iptables -X
    [root@salt ~]# iptables -F

## Start salt-minion on server1, server2

    [root@server1 ~]# systemctl start salt-minion
    [root@server2 ~]# systemctl start salt-minion

## Accept the keys

### On Master

    [root@salt ~]# salt-key -A
    Unaccepted Keys:
    server2
    server1
    Proceed? [n/Y] Y
    Key for minion server1 accepted.
    Key for minion server2 accepted.

### Modify master configuration.

    [root@salt srv]# emacs /etc/salt/master
    file_roots:
      base:
        - /srv/salt/states
    ...
    ...
    pillar_roots:
      base:
        - /srv/salt/pillar

#### Create folders

    [root@salt srv]# mkdir -p /srv/salt/states
    [root@salt srv]# mkdir -p /srv/salt/pillar

#### Restart salt-master

    [root@salt srv]# systemctl restart salt-master
