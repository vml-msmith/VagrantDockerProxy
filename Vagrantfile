# -*- mode: ruby -*-
# vi: set ft=ruby :
hostname = 'vagrant.dev'
memory = 4096
cpus = 2

$script = <<SCRIPT
echo I am provisioning...
date > /etc/vagrant_provisioned_at

curl -SLo "jet-1.4.0.tar.gz" "https://s3.amazonaws.com/codeship-jet-releases/1.4.0/jet-linux_amd64_1.4.0.tar.gz"
sudo tar -xaC /usr/local/bin -f jet-1.4.0.tar.gz
sudo chmod +x /usr/local/bin/jet

cp -r /opt/ssh/* /home/vagrant/.ssh/

curl -L https://github.com/docker/compose/releases/download/1.7.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version

SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = 'ubuntu/trusty64'
  #config.vm.box = 'hashicorp/precise64'
  # Networking
  config.vm.hostname = hostname
  config.vm.network :private_network,
    # https://github.com/oscar-stack/vagrant-auto_network
    :auto_network => true

  # Synced folders.
  opts = {
    create: true,
    type: 'nfs',
    rsync__exclude: ['.idea/', '.git/'],
    rsync__args: ['--verbose', '--archive', '--delete', '-z']
  }

  # Disable default synced folder.
  config.vm.synced_folder '.', '/vagrant', disabled: true
  # Project/site files.
  config.vm.synced_folder 'Sites', '/opt/sites', opts
  config.vm.synced_folder 'bin', '/opt/bin', opts
  # Docker files.
  #  config.vm.synced_folder './provision/', '/opt/provision', opts

  config.vm.synced_folder "~/.ssh", "/opt/ssh"

  # Vagrant provider configuration.
  config.vm.provider :virtualbox do |v|
    v.customize ['modifyvm', :id, '--memory', memory]
    v.cpus = cpus
    v.name = hostname
  end

  config.vm.provision "docker" do |d|
    d.pull_images "jwilder/nginx-proxy"
    d.run "jwilder/nginx-proxy",
          args: "-p 80:80 -p 443:443 -v /var/run/docker.sock:/tmp/docker.sock -t",
          daemonize: true
  end

  config.vm.provision "shell", inline: $script, keep_color: true
end
