# Create a minimal Ubuntu box
Vagrant.require_version ">= 1.8.4"
Vagrant.configure(2) do |config|

     if Vagrant.has_plugin?("vagrant-timezone")
        config.timezone.value = :host
      end

    config.vm.box = "ubuntu/trusty32" # Use a 32bit version, so everybody can run the box      
    config.vm.synced_folder "elastic-stack/", "/elastic-stack/", :mount_options => ["dmode=777","fmode=666"]
	config.vm.network :forwarded_port, guest: 9200, host: 9200
	config.vm.network :forwarded_port, guest: 9300, host: 9300
	config.vm.network :forwarded_port, guest: 5601, host: 5601
    
    # Configure the VirtualBox parameters
    config.vm.provider "virtualbox" do |vb|
        vb.name = "elastic-stack"
        vb.cpus = 4
        vb.customize [ "modifyvm", :id, "--memory", "4096" ]
    end


    # Configure the box with Ansible
    config.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "/elastic-stack/0_install.yml"
    end


end
