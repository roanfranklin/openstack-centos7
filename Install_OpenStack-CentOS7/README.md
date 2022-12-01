yum update -y
reboot


yum install -y centos-release-openstack-rocky
yum update -y
yum install -y openstack-packstack

sudo setenforce 0

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

packstack --allinone --provision-demo=n --os-neutron-ovn-bridge-mappings=extnet:br-ex --os-neutron-ovn-bridge-interfaces=br-ex:eno1

systemctl stop NetworkManager.service 
systemctl disable NetworkManager.service

packstack --allinone --os-neutron-l2-agent=openvswitch --os-neutron-ml2-mechanism-drivers=openvswitch --os-neutron-ml2-tenant-network-types=vxlan --os-neutron-ml2-type-drivers=vxlan,flat --provision-demo=n --os-neutron-ovs-bridge-mappings=extnet:br-ex --os-neutron-ovs-bridge-interfaces=br-ex:eno1

echo "DEVICE=br-ex
DEVICETYPE=ovs
TYPE=OVSBridge
BOOTPROTO=static
IPADDR=192.168.0.254
NETMASK=255.255.255.0
GATEWAY=192.168.0.254
DNS1=192.168.0.254
DNS2=8.8.8.8
DNS3=1.1.1.1
ONBOOT=yes" > /etc/sysconfig/network-scripts/ifcfg-br-ex

cp /etc/sysconfig/network-scripts/ifcfg-eno1 /etc/sysconfig/network-scripts/bkp-eno1

echo "DEVICE=eno1
TYPE=OVSPort
DEVICETYPE=ovs
OVS_BRIDGE=br-ex
ONBOOT=yes" > /etc/sysconfig/network-scripts/ifcfg-eno1

echo 'DEVICE=bond0
DEVICETYPE=ovs
TYPE=OVSPort
OVS_BRIDGE=br-ex
ONBOOT=yes
BONDING_MASTER=yes
BONDING_OPTS="mode=802.3ad"' > /etc/sysconfig/network-scripts/ifcfg-bond0

reboot

