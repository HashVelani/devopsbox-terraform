Vagrant.configure("2") do |config|

  config.vm.box = "generic/centos7"
  
  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.synced_folder "\data", "/data"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end

# require plugin https://github.com/leighmcculloch/vagrant-docker-compose
config.vagrant.plugins = "vagrant-docker-compose"

# install docker and docker-compose
config.vm.provision :docker
config.vm.provision :docker_compose

config.vm.provider "virtualbox" do |vb|
  vb.customize ["modifyvm", :id, "--ioapic", "on"]
  vb.customize ["modifyvm", :id, "--memory", "2048"]
  vb.customize ["modifyvm", :id, "--cpus", "2"]
end

config.vm.network "forwarded_port", guest: 80, host: 8080
  
  config.vm.provision "shell", inline: <<-SHELL
	
    yum update -y
    yum install -y yum-utils
    yum install -y git
    yum install awscli -y
    yum-config-manager --add-repo https://rpm.releases.hashicorp.com/RHEL/hashicorp.repo
    yum -y install terraform


    groupadd docker
    usermod -aG docker $USER


  SHELL
end
