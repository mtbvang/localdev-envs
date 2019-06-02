# -*- mode: ruby -*-
# vi: set ft=ruby :

PROJECT_NAME = ENV['PROJECT_NAME'] || File.basename(File.expand_path(File.dirname(__FILE__)))
ANSIBLE_GALAXY_FORCE = ENV['ANSIBLE_GALAXY_FORCE'] || "--force"

Vagrant.configure("2") do |config|

  ENV['VAGRANT_DEFAULT_PROVIDER'] = 'docker'

  config.vm.provider "docker" do |d|
    d.build_dir = "provisioning"
    d.build_args = ["--build-arg", "DOCKER_GROUP_ID=986"]
    d.dockerfile = "Dockerfile.vagrant"
    d.has_ssh = true
    d.volumes = ["/var/run/docker.sock:/var/run/docker.sock"]
  end

  @syncfolder_type = 'virtualbox'
  if Vagrant::Util::Platform.windows? then
    syncfolder_type = 'nfs'
  end

  config.vm.synced_folder '../', '/vagrant', type: syncfolder_type , disabled: false

  config.vm.provision :ansible_local do |ansible|
    ansible.verbose = "v"
    ansible.install_mode = "pip"
    ansible.version = "2.4.2.0"
    ansible.playbook = "#{PROJECT_NAME}/provisioning/playbook.yml"
    ansible.galaxy_role_file = "#{PROJECT_NAME}/provisioning/requirements.yml"
    ansible.galaxy_roles_path = "#{PROJECT_NAME}/provisioning/.roles"
    ansible.galaxy_command = "ansible-galaxy install --ignore-certs --role-file=%{role_file} --roles-path=%{roles_path} #{ANSIBLE_GALAXY_FORCE}"
    ansible.become = true
  end
  
  if Vagrant.has_plugin?("vagrant-cachier")
    config.proxy.enabled = { svn: false, docker: false }
  end

end