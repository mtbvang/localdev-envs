# -*- mode: ruby -*-
# # vi: set ft=ruby :

PROJECT_NAME = ENV['PROJECT_NAME'] || File.basename(File.expand_path(File.dirname(__FILE__)))
ANSIBLE_VERSION = ENV['ANSIBLE_VERSION'] || '2.5.4'
ANSIBLE_GALAXY_FORCE = ENV['ANSIBLE_GALAXY_FORCE'] || "--force"
IP_BASE = 10
VB_GUEST = ENV['VB_GUEST'] == 'true' ? true : false

Vagrant.configure(2) do |config|

  # The admin VM that is seperate from the kubernetes VMs and contains the development tools.
  config.vm.define "localdev" do |vms|
    
    #vms.vm.box = "boxcutter/ubuntu1804-desktop"
    vms.vm.box = "juguerre/ubuntu-desktop-18.04"
    vms.vm.hostname = "localdev-dev.vagrant.net"
    
    vms.vm.network "private_network", ip: "172.42.42.#{IP_BASE}", netmask: "255.255.255.0", auto_config: true

    @syncfolder_type = 'virtualbox'
    if Vagrant::Util::Platform.windows? then
      syncfolder_type = 'nfs'
    end
    vms.vm.synced_folder '../', '/vagrant', type: syncfolder_type , disabled: false
    #vms.vm.synced_folder "~/.m2", '/home/vagrant/.m2', type: syncfolder_type , disabled: false
    #vms.vm.synced_folder "~/.ssh", '/.ssh', type: syncfolder_type , disabled: false

    vms.vm.provider "virtualbox" do |v|
      v.name = "localdev-python"
      v.memory = 2048
      v.gui = false
    end

    vms.vm.provision "ansible", type: :ansible_local do |ansible|
      ansible.verbose = "v"
      ansible.install_mode = "pip"
      ansible.version = ANSIBLE_VERSION
      ansible.playbook = "/vagrant/#{PROJECT_NAME}/provisioning/playbook.yml"
      ansible.galaxy_role_file = "/vagrant/#{PROJECT_NAME}/provisioning/requirements.yml"
      ansible.galaxy_roles_path = "/vagrant/#{PROJECT_NAME}/provisioning/.roles"
      ansible.galaxy_command = "ansible-galaxy install --ignore-certs --role-file=%{role_file} --roles-path=%{roles_path} #{ANSIBLE_GALAXY_FORCE}"
      ansible.become = true
    end
  end

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
  end

  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = VB_GUEST
  end

  if Vagrant.has_plugin?("vagrant-hostmanager")
    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
    config.hostmanager.manage_guest = true
  end

end
