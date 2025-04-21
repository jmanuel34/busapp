Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"

  config.vm.define "ansible" do |ansible|
    ansible.vm.hostname = "ansible"
    ansible.vm.network "private_network", ip: "192.168.56.5"
    ansible.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
    end
    ansible.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y ansible python3
    SHELL
  end

  config.vm.define "manager" do |manager|
    manager.vm.hostname = "manager"
    manager.vm.network "private_network", ip: "192.168.56.10"
    manager.vm.network "forwarded_port", guest: 80, host: 8080, auto_correct: true
    manager.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 2
    end
    manager.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y docker.io
      usermod -aG docker vagrant
      systemctl enable docker
    SHELL
  end

  config.vm.define "worker1" do |worker1|
    worker1.vm.hostname = "worker1"
    worker1.vm.network "private_network", ip: "192.168.56.11"
    worker1.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 2
    end
    worker1.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y docker.io
      usermod -aG docker vagrant
      systemctl enable docker
    SHELL
  end

  config.vm.define "worker2" do |worker2|
    worker2.vm.hostname = "worker2"
    worker2.vm.network "private_network", ip: "192.168.56.12"
    worker2.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 2
    end
    worker2.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y docker.io
      usermod -aG docker vagrant
      systemctl enable docker
    SHELL
  end
end
