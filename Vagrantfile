Vagrant.configure("2") do |config|

  # configure two Machines with Ubuntu 22.04
  vm_desc = [ ["say01srvansible", "192.168.1.101" ], ["say01srvsrt", "192.168.1.111"] ]
  vm_desc.each do |nam, add|
    config.vm.define "#{nam}" do |node|
      node.vm.box = "ubuntu/jammy64"
      node.vm.network "private_network", ip: "#{add}", virtualbox__intnet: "say01.local"
      node.vm.hostname = "#{nam}.say01.local"
      node.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
        vb.name = "#{nam}"
      end
      # node.vm.provision "shell", inline: <<-SHELL
      #   apt-get update && apt-get upgrade -y
      #   sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
      #   systemctl restart sshd
      # SHELL
    end
  end

  # configure three ubuntu machines as restreamserver
  (1..3).each do |i|
    config.vm.define "fsn01srvstr0#{i}" do |node|
      node.vm.box = "ubuntu/jammy64"
      node.vm.network "private_network", ip: "192.168.1.2#{i}", virtualbox__intnet: "say01.local"
      node.vm.hostname = "fsn01srvstr0#{i}.say01.local"
      node.vm.provider "virtualbox" do |vb|
        vb.memory = "1024"
        vb.name = "fsn01srvstr0#{i}"
      end
    end
  end

  # configure three microsoft windows 10 machines for OBS Studio
  (1..3).each do |i|
    config.vm.define "say01pcgobs0#{i}" do |node|
      node.vm.box = "gusztavvargadr/windows-10"
      node.vm.network "private_network", ip: "192.168.1.1#{i}", virtualbox__intnet: "say01.local"
      node.vm.hostname = "say01pcgobs0#{i}"
      node.vm.provider "virtualbox" do |vb|
        vb.memory = "4096"
        vb.name = "say01pcgobs0#{i}"
      end
    end
  end

end
