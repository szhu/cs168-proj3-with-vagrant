# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = '2'

$script = <<SCRIPT
shopt -s dotglob

if ! test -e /home/cs168/public/Vagrantfile; then
  echo 1>&2 "Oh no, Vagrant did not connect shared folders properly."
  echo 1>&2 "I'm not sure what went wrong. Is Vagrant properly installed?"
  exit 1
elif ! test -e /home/cs168/public-bak; then
  echo 1>&2 "Oh no, you forgot to rename your public folder to public-bak."
  echo 1>&2
  echo 1>&2 "Here's what you need to do:"
  echo 1>&2 "1. Go to VirtualBox and turn the VM off."
  echo 1>&2 "2. In VirtualBox VM settings, remove all shared folders."
  echo 1>&2 "3. Start up the VM in VirtualBox."
  echo 1>&2 "4. Open a terminal and: mv public public-bak"
  echo 1>&2 "5. From the host: vagrant reload --provision"
  exit 1
fi

echo 1>&2 "Moving files into shared folder..."
mv -f -- /home/cs168/public-bak/* /home/cs168/public/
rmdir -- /home/cs168/public-bak

echo "Setup completed successfully!"
echo "You can now edit your project files in the host filesystem."
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Box
  config.vm.box = 'base'
  config.vm.provider 'virtualbox' do |vb|
    vb.name = 'cs168proj3'
    vb.gui = false
  end

  # Network
  config.vm.network :private_network,
    ip: '172.16.122.2', netmask: '255.255.255.0', auto_config: false

  # SSH
  config.ssh.host = '172.16.122.2'
  config.ssh.port = '22'
  config.ssh.username = 'cs168'
  config.ssh.password = 'gobears!'
  config.ssh.forward_agent = true

  # Files
  config.vm.provision "shell", inline: $script, privileged: false
  config.vm.synced_folder '.', '/home/cs168/public', id: 'cs168proj3'
end
