## Configuration of target hosts
```bash
[root@ansible-demo-1 opt]# cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
192.168.56.11 ansible-demo-1
192.168.56.12 ansible-demo-2
192.168.56.13 ansible-demo-3
[root@ansible-demo-1 opt]# cat /etc/hostname
ansible-demo-1
```

## Network configuration of target hosts (interface enp0s3 - NAT, dhcp. interface enp0s8 - accessible from host)
NO network interfaces UUID here!

```bash
[root@ansible-demo-1 opt]# cat /etc/sysconfig/network-scripts/ifcfg-enp0s3
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
BOOTPROTO=dhcp
DEFROUTE=yes
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=enp0s3
DEVICE=enp0s3
ONBOOT=yes

[root@ansible-demo-1 opt]# cat /etc/sysconfig/network-scripts/ifcfg-enp0s8
TYPE=Ethernet
PROXY_METHOD=none
BROWSER_ONLY=no
IPV4_FAILURE_FATAL=no
IPV6INIT=yes
IPV6_AUTOCONF=yes
IPV6_DEFROUTE=yes
IPV6_FAILURE_FATAL=no
IPV6_ADDR_GEN_MODE=stable-privacy
NAME=enp0s8
DEVICE=enp0s8
ONBOOT=yes
IPADDR=192.168.56.11
```
## Configuration of authorized_keys
```bash
[root@ansible-demo-1 opt]# cat /root/.ssh/authorized_keys
ssh-rsa AAAAB3Nza...ANSIBLE_HOST_PUB_KEY root@ansiblevm
ssh-rsa AAAABC1yc...YOUR_DESKTOP_HOST_PUB_KEY root@mynote
```
