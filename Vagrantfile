# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # config.vm.provision "shell", inline: "sudo curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo"
  config.vm.box = "centos7"

  config.vm.define "master", primary: true do |master|
    master.vm.hostname = "master-node"
    master.vm.network "private_network", ip: "192.168.33.10"
    master.vm.provision "shell", inline: <<-SHELL
      # 启动docker swarm
      sudo docker swarm init --advertise-addr eth1
    SHELL
  end

  config.vm.define "nodeA" do |nodeA|
    nodeA.vm.hostname = "worker-nodeA"
    nodeA.vm.network "private_network", ip: "192.168.33.11"
    nodeA.vm.provision "shell", inline: <<-SHELL
      # 启动docker swarm
      docker swarm join \
        --token SWMTKN-1-5p2v34obleqckqx87v46kxksf768eqg2ew0qie7a3nig8ny64w-0z3kv1vi8sx9ema0ripoa7gs9 \
        192.168.33.10:2377
    SHELL
  end

  config.vm.define "nodeB" do |nodeB|
    nodeB.vm.hostname = "worker-nodeB"
    nodeB.vm.network "private_network", ip: "192.168.33.12"
    nodeB.vm.provision "shell", inline: <<-SHELL
      # 启动docker swarm
      docker swarm join \
        --token SWMTKN-1-5p2v34obleqckqx87v46kxksf768eqg2ew0qie7a3nig8ny64w-0z3kv1vi8sx9ema0ripoa7gs9 \
        192.168.33.10:2377
    SHELL
  end

  config.vm.define "nodeC" do |nodeC|
    nodeC.vm.hostname = "worker-nodeC"
    nodeC.vm.network "private_network", ip: "192.168.33.13"
    nodeC.vm.provision "shell", inline: <<-SHELL
      # 启动docker swarm
      docker swarm join \
        --token SWMTKN-1-5p2v34obleqckqx87v46kxksf768eqg2ew0qie7a3nig8ny64w-0z3kv1vi8sx9ema0ripoa7gs9 \
        192.168.33.10:2377
    SHELL
  end


  # config.vm.box = "base"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    # vb.gui = true
  
    # Customize the amount of memory on the VM:
    # vb.memory = 1024
    vb.cpus = 2
  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    # Docker need this config
    # Open these
    sudo echo '1' > /proc/sys/net/bridge/bridge-nf-call-iptables
    sudo echo '1' > /proc/sys/net/bridge/bridge-nf-call-ip6tables
  SHELL
end
