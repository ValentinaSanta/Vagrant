# -*- mode: ruby -*-
# vi: set ft=ruby :

#cliente
CLIENT_SCRIPT = <<EOF.freeze
echo "Preparing node..."
# ensure the time is up to date
sudo apt-get update
sudo apt-get install -y ntpdate 
echo '192.168.50.2 NTP-server-host' > /etc/hosts
sudo ntpdate NTP-server-host
sudo timedatectl set-nyp off
sudo apt-get install -y ntp
echo 'server NTP-server-host prefer iburst' > /etc/ntp.conf
sudo service ntp restart
EOF

#servidor
TI_SCRIPT = <<EOF.freeze
echo "Preparing node..."
# ensure the time is up to date
sudo apt-get update 
sudo apt-get install -y ntp
sudo service ntp restart
sudo ufw allow from any to any port 123 proto udp
EOF

def set_hostname(server)
server.vm.provision 'shell', inline: "hostname #{server.vm.hostname}"
end

Vagrant.configure(2) do |config|
# Defines a configuration environment for the webapp locally for testing

    # TI 192.168.50.0/24
    config.vm.define 'nodo-ti' do |n|
    n.vm.network "private_network", ip: "192.168.50.2", netmask: "24"
    n.vm.box = 'bento/ubuntu-18.04'
    n.vm.box_version = '202007.17.0'
    n.vm.hostname = 'nodo-ti'
    n.vm.provision :shell, inline: TI_SCRIPT.dup
    set_hostname(n)
    end

    # REPUESTOS
    config.vm.define 'nodo-repuesto' do |n|
    n.vm.network "private_network", ip: "192.168.51.2", netmask: "24"
    n.vm.box = 'bento/ubuntu-18.04'
    n.vm.box_version = '202007.17.0'
    n.vm.hostname = 'nodo-repuesto'
    n.vm.provision :shell, inline: CLIENT_SCRIPT.dup
    set_hostname(n)
    end

    # VENTAS
    config.vm.define 'nodo-ventas' do |n|
    n.vm.network "private_network", ip: "192.168.52.2", netmask: "24"
    n.vm.box = 'bento/ubuntu-18.04'
    n.vm.box_version = '202007.17.0'
    n.vm.hostname = 'nodo-ventas'
    n.vm.provision :shell, inline: CLIENT_SCRIPT.dup
    set_hostname(n)
    end

    # ADMIN
    config.vm.define 'nodo-admin' do |n|
    n.vm.network "private_network", ip: "192.168.53.2", netmask: "24"
    n.vm.box = 'bento/ubuntu-18.04'
    n.vm.box_version = '202007.17.0'
    n.vm.hostname = 'nodo-admin'
    n.vm.provision :shell, inline: CLIENT_SCRIPT.dup
    set_hostname(n)
    end

    # RESTAURACION
    config.vm.define 'nodo-restauracion' do |n|
    n.vm.network "private_network", ip: "192.168.54.2", netmask: "24"
    n.vm.box = 'bento/ubuntu-18.04'
    n.vm.box_version = '202007.17.0'
    n.vm.hostname = 'nodo-restauracion'
    n.vm.provision :shell, inline: CLIENT_SCRIPT.dup
    set_hostname(n)
    end
end
    