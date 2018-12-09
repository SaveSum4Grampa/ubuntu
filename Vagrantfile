# This guide is optimized for Vagrant 1.7 and above.
# Although versions 1.6.x should behave very similarly, it is recommended
# to upgrade instead of disabling the requirement below.
Vagrant.require_version ">= 1.7.0"

Vagrant.configure(2) do |config|

  config.vm.box = "bento/ubuntu-18.04"

  # Disable the new default behavior introduced in Vagrant 1.7, to
  # ensure that all Vagrant machines will use the same SSH key pair.
  # See https://github.com/mitchellh/vagrant/issues/5005
  config.ssh.insert_key = false
  
  config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.network :forwarded_port, guest: 22, host: 2223, id: 'ssh'

  config.vm.network "private_network", ip: "192.168.33.15"
  
  config.vm.synced_folder ".", "/vagrant", type: 'virtualbox'
  
  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  
  config.vm.provider :virtualbox do |vb|
    # Use VBoxManage to customize the VM.
    # For example to change memory or number of CPUs:
    vb.customize ["modifyvm", :id, "--memory", "4096"]
    vb.customize ["modifyvm", :id, "--cpus", "1"]
  end

  config.vm.provision "ansible_local" do |ansible|
    ansible.verbose = "vvvv"
    ansible.playbook = "playbooks/setup-everything.yml"
  end
end