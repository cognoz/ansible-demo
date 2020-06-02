## Basic stuff for ansible lesson
Here ull find:
- inventory/playbooks samples
- vars
- description

## Inventory 
inventory.ini - some cool stuff with parents/sequence
simple-inv.ini - simpler version of it

## Playbooks
consul-playbook for consul and patroni-playbook for - u get it

## Howto
### Deploy host
```bash
mkdir /home/patroni
mkdir -p /etc/ansible/roles/

#Pip section
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python get-pip.py
pip install virtualenv
virtualenv /home/patroni/demo_venv
source /home/patroni/demo_venv/bin/activate
pip install ansible==2.8.5
yum -y install python-netaddr #system-wide, some bugs with ansible invocation of pip package

#Roles 
ansible-galaxy search patroni
ansible-galaxy install -p /etc/ansible/roles/ kostiantyn-nemchenko.patroni
ansible-galaxy search consul  #too many
ansible-galaxy info brianshumate.consul
ansible-galaxy install -p /etc/ansible/roles/ brianshumate.consul
ansible-galaxy list

cp vars.yml inventoty.ini consul-playbook.yml patroni-playbook.yml /home/patroni
```

Now we need update configuration - vars/invenory 
```bash
cd /home/patroni
vim vars.yml
vim inventory.ini
```

### Target hosts 1-3
#### Part 1
First of all add ssh pubkey from deployhost to target host's authorized\_keys file
Next, configure hostnames and /etc/hosts resolv
Finally, configure network interfaces. 
[Example of configuration](prepare_hosts.md)
#### Part 2
Disable firewalld due to consul intercommunications
```bash
systemctl stop firewalld
systemctl disable firewalld
```

Don't forget to add deployhost's public ssh-rsa key to /root/.ssh/authorized\_keys on target hosts.


### Install consul
```bash
ansible-playbook -vv -i inventory.ini -e @vars.yml consul-playbook.yml 
```
### Check consul
```bash
#Open in browser
http://TARGETNODE1-IP:8500/ui/dc1/nodes

#Or in CLI on any node 
consul members -http-addr=http://TARGETNODE1-IP:8500

#if you forgot to disable firewalld you'll see only 1 member in list
#In that case just stop/disable firewalld and restart consul everywhere
#via command
systemctl restart consul
```

### Install patroni
```bash
ansible-playbook -vv -i inventory.ini -e @vars.yml patroni-playbook.yml
```

### Check Patroni
```bash
patronictl -c /etc/patroni/TARGETNODE1-IP.yml list main
psql -Upostgres -W
supersecretpostgrespasswd

\l
create database test2;
\l
\q
```
