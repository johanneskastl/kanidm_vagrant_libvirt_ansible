Vagrant.configure("2") do |config|

  ###################################################################################
  config.vm.define "kanidm-client" do |node|

    # which image to use
    node.vm.box = "opensuse/Leap-15.6.x86_64"

    # sizing of the VMs
    node.vm.provider "libvirt" do |lv|
      lv.random_hostname = true
      lv.memory = 1024
      lv.cpus = 2
    end

    # set the hostname
    node.vm.hostname = "kanidm-client"

    # disable shared folders
    node.vm.synced_folder ".", "/vagrant", disabled: true

  end # config.vm.define agents

  ###################################################################################
  # name the VMs
  config.vm.define "kanidm-server" do |node|

    # which image to use
    node.vm.box = "opensuse/Tumbleweed.x86_64"

    # sizing of the VMs
    node.vm.provider "libvirt" do |lv|
      lv.random_hostname = true
      lv.memory = 4096
      lv.cpus = 2
    end

    # set the hostname
    node.vm.hostname = "kanidm-server"

    # disable shared folders
    node.vm.synced_folder ".", "/vagrant", disabled: true

    # Ansible
    node.vm.provision "ansible" do |ansible|
      ansible.compatibility_mode = "2.0"
        ansible.limit = "all"
      ansible.playbook = "ansible/playbook-vagrant.yml"
    end # node.vm.provision

  end # config.vm.define servers

end # Vagrant.configure
