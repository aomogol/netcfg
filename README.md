Open up a terminal window on your Ubuntu 18.04 server (or log in via secure shell). Change into the /etc/netplan directory with the command cd /etc/netplan. Issue the command ls and you should see a file named 50-cloud-init.yaml. If you don't also see a file named 01-netcfg.yaml, create it with the command sudo touch 01-netcfg.yaml. Before we edit that file, we need to know the name of our networking interface. Issue the command ip a and you should see your system network interface listed by name

What's crucial about the layout of this file is not using the exact same spacing as my example, but that you're consistent. If you're not consistent with your indents, the file will not work. What you see in that sample file is all you need to configure that static IP address. Do notice, you aren't setting the address is the same fashion as you did with Ubuntu 16.04. With the old method, you set IP address and netmask like so:

address = 192.168.1.206
netmask = 255.255.255.0

With netplan, these are set with a single line:

addresses : [192.168.1.206/24]

Restarting/testing networking

With the new method, you must restart networking using netplan. So once you've configured your interface, issue the command:

sudo netplan apply

The above command will restart networking and apply the new configuration. You shouldn't see any output. If networking fails to function properly, you can issue the command:

sudo netplan --debug apply


