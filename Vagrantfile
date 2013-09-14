Vagrant.configure("2") do |config|
  config.vm.network :private_network, ip: "192.168.111.222"
  config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.box = "precise64"


  config.vm.provider "virtualbox" do |vb|
  #   v.name = "Emberjs_environment"
     vb.customize ["modifyvm", :id, "--memory", "512"]
  end

  # Synced folders
  config.vm.synced_folder "ansible/", "/ansible"
  config.vm.synced_folder "www/", "/var/www"

  # Add ansible inside the virtual machine, run ansible-playbook against /ansible/playbook.yml
  config.vm.provision :shell,
    :inline => "sudo apt-get update && sudo apt-get -y install python-software-properties && sudo add-apt-repository -y ppa:rquillo/ansible && sudo apt-get -y install ansible && echo localhost > /etc/ansible/hosts && sudo ansible-playbook /ansible/playbook.yml --connection=local && sudo reboot "
end
