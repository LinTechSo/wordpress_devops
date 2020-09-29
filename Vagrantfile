# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.hostname = "wordpress"
  config.vm.network :private_network, ip: "192.168.121.90"
  config.vm.provision :shell, :inline => "sudo sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config; sudo systemctl restart sshd;", run: "always" 
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.provider :virtualbox do |v|
    v.memory = 2048
  end

  # Ansible provisioning
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "wordpress/site.yml"
    ansible.inventory_path = "inventory/hosts"
    ansible.limit = "all"
  end
end
