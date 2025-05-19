-- mode: ruby --
vi: set ft=ruby :
Vagrant.configure("2") do |config|

shared_host_folder = "./shared"

config.vm.define "machine1" do |machine1|
machine1.vm.box = "generic/debian12"
machine1.vm.box_version = "4.3.12"

machine1.vm.hostname = "machine1"
machine1.vm.network "private_network", ip: "192.168.56.10"
machine1.vm.synced_folder shared_host_folder, "/mnt/shared", type: "rsync"
end

config.vm.define "machine2" do |machine2|
machine2.vm.box = "generic/debian12"
machine2.vm.box_version = "4.3.2"

machine2.vm.hostname = "machine2"
machine2.vm.network "private_network", ip: "192.168.56.11"
machine2.vm.synced_folder shared_host_folder, "/mnt/shared", type: "rsync"
end

config.vm.synced_folder ".", "/vagrant", disabled: true

config.vm.provider "virtualbox" do |vb|
vb.gui = true
vb.memory = "1024"
vb.cpus = 2
end

config.vm.provision "shell", inline: <<-SHELL
echo "Install htop..."
apt-get update
apt-get install -y htop
SHELL

#wget writes its output to stderr by default, even if everything went well
config.vm.provision "shell", inline: <<-SHELL
echo "Download TempleOS..."
wget https://templeos.org/Downloads/TempleOS.ISO 2>&1
SHELL
end