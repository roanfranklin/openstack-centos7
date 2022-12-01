rm -rf /etc/sysconfig/network-scripts/ifcfg-br-ex
rm -rf /etc/sysconfig/network-scripts/ifcfg-bond0

echo "DEVICE=eno1
NAME=eno1
TYPE=Ethernet
BOTOTPROTO=static
IPADDR=192.168.0.253
NETMASK=255.255.255.0
GATEWAY=192.168.0.254
DNS1=192.168.0.254
DNS2=8.8.8.8
DNS3=1.1.1.1
ONBOOT=yes" > /etc/sysconfig/network-scripts/ifcfg-eno1

reboot


yum remove -y openstack-packstack
yum remove -y centos-release-openstack-rocky
