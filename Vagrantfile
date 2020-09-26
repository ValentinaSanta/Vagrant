# -*- mode: ruby -*-
# vi: set ft=ruby :

#Red: 192.168.1.0/24 (clase c)
#TI (10 host): 192.168.1.1 - 192.168.1.10
#Repuestos (3 host): 192.168.1.11 - 192.168.1.13
#Ventas (10 host): 192.168.1.14 - 192.168.1.23
#Taller (5 host): 192.168.1.24 - 192.168.1.28
#Restauración (5 host): 192.168.1.29 - 192.168.1.33
#Servidor: 192.168.1.34


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


   # SERVER 
   config.vm.define 'nodo-server' do |n|
    n.vm.network "private_network", ip: "192.168.1.34"
    n.vm.box = 'bento/ubuntu-18.04'
    n.vm.box_version = '202007.17.0'
    n.vm.hostname = 'nodo-server'
    n.vm.provision :shell, inline: TI_SCRIPT.dup
    set_hostname(n)
    end

    # TI 
    config.vm.define 'nodo-ti' do |n|
    n.vm.network "private_network", ip: "192.168.1.1"
    n.vm.box = 'bento/ubuntu-18.04'
    n.vm.box_version = '202007.17.0'
    n.vm.hostname = 'nodo-ti'
    n.vm.provision :shell, inline: CLIENT_SCRIPT.dup
    set_hostname(n)
    end

    # REPUESTOS
    config.vm.define 'nodo-repuesto' do |n|
    n.vm.network "private_network", ip: "192.168.1.11"
    n.vm.box = 'bento/ubuntu-18.04'
    n.vm.box_version = '202007.17.0'
    n.vm.hostname = 'nodo-repuesto'
    n.vm.provision :shell, inline: CLIENT_SCRIPT.dup
    set_hostname(n)
    end

    # VENTAS
    config.vm.define 'nodo-ventas' do |n|
    n.vm.network "private_network", ip: "192.168.1.14"
    n.vm.box = 'bento/ubuntu-18.04'
    n.vm.box_version = '202007.17.0'
    n.vm.hostname = 'nodo-ventas'
    n.vm.provision :shell, inline: CLIENT_SCRIPT.dup
    set_hostname(n)
    end

    # TALLER
    config.vm.define 'nodo-tallern' do |n|
    n.vm.network "private_network", ip: "192.168.1.24"
    n.vm.box = 'bento/ubuntu-18.04'
    n.vm.box_version = '202007.17.0'
    n.vm.hostname = 'nodo-taller'
    n.vm.provision :shell, inline: CLIENT_SCRIPT.dup
    set_hostname(n)
    end

    # RESTAURACION
    config.vm.define 'nodo-restauracion' do |n|
    n.vm.network "private_network", ip: "192.168.1.29"
    n.vm.box = 'bento/ubuntu-18.04'
    n.vm.box_version = '202007.17.0'
    n.vm.hostname = 'nodo-restauracion'
    n.vm.provision :shell, inline: CLIENT_SCRIPT.dup
    set_hostname(n)
    end
end
    