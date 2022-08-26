Vagrant.configure("2") do |config|
	
	config.vm.define "ansible" do |ansible|
	  ansible.vm.provider :virtualbox do |vb|
	    vb.customize ["modifyvm", :id, "--memory", "2048"]
        vb.customize ["modifyvm", :id, "--cpus", "2"]
        end
	  ansible.vm.box = "debian/buster64"
	  ansible.vm.network "public_network", bridge: "Realtek PCIe GbE Family Controller"
	  ansible.vm.network "private_network", ip: "192.168.10.20"
	  ansible.vm.hostname = "ansible"
	  ansible.vm.synced_folder ".", "/vagrant", disabled: true
	  ansible.vm.provision "shell", inline: <<-SHELL
		sudo apt update && sudo apt upgrade -y
		sudo apt install vim git ansible -y
		sudo useradd -s /bin/bash -G wheel -m ansible -p Hz6AQRa6WPcEc
		sudo mkdir /home/ansible/.ssh
		sudo ssh-keygen -t ed25519 -f /home/ansible/.ssh/id_ed25519 -N ""
		sudo git clone https://github.com/rudolf-gati-7734/ansible-docker-deployment.git /home/ansible/ansible-docker-deployment
		sudo chown -R ansible:ansible /home/ansible/
	  SHELL
	end

	config.vm.define "server" do |server|
	  server.vm.provider :virtualbox do |vb|
	    vb.customize ["modifyvm", :id, "--memory", "1024"]
        vb.customize ["modifyvm", :id, "--cpus", "1"]
        end
	  server.vm.box = "debian/buster64"
	  server.vm.network "public_network", bridge: "Realtek PCIe GbE Family Controller"
	  server.vm.network "private_network", ip: "192.168.10.21"
	  server.vm.synced_folder ".", "/vagrant", disabled: true
	  server.vm.hostname = "server"
	  server.vm.provision "shell", inline: <<-SHELL
		sudo apt update && sudo apt upgrade -y
		sudo useradd -s /bin/bash -G wheel -m ansible -p Hz6AQRa6WPcEc
	  SHELL
	end
	
end