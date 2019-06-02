# -*- mode: ruby -*-
# vi: set ft=ruby :

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

  config.vm.provision :ansible_local do |ansible|
    ansible.verbose = "v"
    ansible.install_mode = "pip"
    ansible.version = "2.4.2.0"
    ansible.playbook = "provisioning/playbook.yml"
    ansible.galaxy_role_file = "provisioning/requirements.yml"
    ansible.galaxy_roles_path = "provisioning/.roles"
    ansible.galaxy_command = "ansible-galaxy install --ignore-certs --role-file=%{role_file} --roles-path=%{roles_path} #{ANSIBLE_GALAXY_FORCE}"
    ansible.become = true
  end
  
  if Vagrant.has_plugin?("vagrant-cachier")
    config.proxy.enabled = { svn: false, docker: false }
  end

  
end