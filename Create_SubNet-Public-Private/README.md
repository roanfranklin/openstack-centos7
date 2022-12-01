source keystonerc_admin


neutron net-create external_network --provider:network_type flat --provider:physical_network extnet  --router:external
neutron subnet-create --name public_subnet --enable_dhcp=False --allocation-pool=start=192.168.0.100,end=192.168.0.120 --gateway=192.168.0.254 external_network 192.168.0.0/24

neutron net-create private_network
neutron subnet-create --name private_subnet private_network 192.168.10.0/24 --dns-nameserver 192.168.0.254,8.8.8.8,1.1.1.1

neutron router-create router1
neutron router-gateway-set router1 external_network

neutron router-interface-add router1 private_subnet
