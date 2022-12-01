source keystonerc_admin

curl -OL http://download.cirros-cloud.net/0.5.1/cirros-0.5.1-x86_64-disk.img

openstack image create --public --disk-format qcow2 --container-format bare --file cirros-0.5.1-x86_64-disk.img cirros051

echo -e "user: cirros\npass: gocubsgo"

---

curl -OL https://cloud-images.ubuntu.com/bionic/current/bionic-server-cloudimg-amd64.img

openstack image create --public --disk-format qcow2 --container-format bare --file bionic-server-cloudimg-amd64.img ubuntubionec1804arm64

echo -e "user: ubuntu\npass: PAR DE CHAVE"

---

curl -OL https://cloud-images.ubuntu.com/focal/current/focal-server-cloudimg-arm64.img

openstack image create --public --disk-format qcow2 --container-format bare --file focal-server-cloudimg-arm64.img ubuntufocal2004arm64

---

wget https://cloud.centos.org/centos/8/x86_64/images/CentOS-8-GenericCloud-8.3.2011-20201204.2.x86_64.qcow2

openstack image create --container-format bare --disk-format qcow2 --file CentOS-8-GenericCloud-8.3.2011-20201204.2.x86_64.qcow2 CentOS-8

---

wget http://cloud.centos.org/centos/7/images/CentOS-7-x86_64-GenericCloud.qcow2

openstack image create --container-format bare --disk-format qcow2 --file CentOS-7-x86_64-GenericCloud.qcow2 CentOS-7

---

wget http://cdimage.debian.org/cdimage/openstack/current-10/debian-10-openstack-amd64.qcow2

openstack image create --container-format bare --disk-format qcow2 --file debian-10-openstack-amd64.qcow2 Debian-10