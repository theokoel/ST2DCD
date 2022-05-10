Vagrant.configure("2") do |config|


  config.vm.define "jenkins" do |jenkins|
    jenkins.vm.box = "ubuntu/xenial64"
    jenkins.vm.network "private_network", ip: "192.168.56.101"
    jenkins.vm.network "forwarded_port", guest: 8080, host: 8080
    jenkins.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.cpus = 2
      vb.memory = "4096"
    end
    jenkins.vm.provision "shell" do |shell|
      shell.path = "jenkins.sh"
    end
  end


  config.vm.define "slave" do |slave|
    slave.vm.box = "ubuntu/xenial64"
    slave.vm.network "private_network", ip: "192.168.56.102"
    slave.vm.network "forwarded_port", guest: 8081, host: 8081
    slave.vm.provider "virtualbox" do |vb|
      vb.gui = false
      vb.memory = "2048"
    end
    slave.vm.synced_folder "./data", "/home/vagrant/data"
    slave.vm.provision "shell", inline: <<-SHELL
      apt-get update
    SHELL
  end


end
