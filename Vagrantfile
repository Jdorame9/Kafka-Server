# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

$script = <<-SCRIPT
apt-get update 
sudo apt upgrade

mkdir dockerfolder
cd dockerfolder

sudo apt-get install  curl apt-transport-https ca-certificates software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

sudo apt update
apt-cache policy docker-ce

sudo apt install docker-ce -y
sudo systemctl status docker

sudo curl -L https://github.com/docker/compose/releases/download/1.20.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/bionic64"
  # Checkea las opciones aqui https://www.vagrantup.com/docs/networking/private_network
  config.vm.network "private_network", ip: "10.20.19.97"
  config.vm.box_version = "1.0.282"
  config.vm.synced_folder "./docker","/home/vagrant/docker"
  config.vm.provider "virtualbox" do |vb|
    vb.name = "server-kafka"
    vb.memory = "2048"
  end

  config.vm.provision :shell, :inline => $script
end
