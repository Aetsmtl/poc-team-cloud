This directory contains scripts for KVM environment prequisites on Ubuntu/CentOS server.

1) INSTALLING KVM (minimal : without graphical interface)

to install kvm, run the script istallKvmOnLinux.sh located in poc-team-cloud/setupScripts.
If you are installing on ubuntu server, run the script with the argument "ubuntu".
If you are installing on Centos / RedHat server, run the script without argument

2) CREATE A VIRTUAL NETWORK

You need to attach your VMs or virtual network interface or virtual bridge. We are using virtual bridge in this tuto. You can easily create a bridge with the bridge command "brctl" 
	a) create the bridge bridge_name
	brctl addbr bridge_name
	b) set up the bridge bridge_name with:
		-	network_id: xxx.yyy.zzz.abc (this @ip is the gateway of this virtual network)
		-	subnet_mask: XXX.YYY.ZZZ.ABC

	ifconfig bridge_name network_id/subnet_mask up

3) CONFIGURE ETHERNET TO FORWARD TRAFFIC

- make sure the content of the file /proc/sys/net/ipv4/ip_forward is 1

	 echo "1" > /proc/sys/net/ipv4/ip_forward


- make sure the main ethernet interface cad provide NAT service:

	 iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE