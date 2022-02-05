Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-20.04"

  config.vm.provider :virtualbox do |v|
    v.gui = true
    v.memory = 2048
  end

  # Currently "ubuntu/bionic64" on VirtualBox requires `type: "virtualbox"`
  # to make synced folder works.
  config.vm.synced_folder ".", "/vagrant", type: "virtualbox"

  # Add mangodb repository
  config.vm.provision :shell, inline: "wget -q -O - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key add -"
  config.vm.provision :shell, inline: "sudo sh -c 'echo \"deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/4.4 multiverse\" > /etc/apt/sources.list.d/mongodb-org-4.4.list'"

  # Update repositories
  config.vm.provision :shell, inline: "sudo apt update -y"

  # Upgrade installed packages
  config.vm.provision :shell, inline: "sudo apt upgrade -y"

  # Install mangodb dependencies
  config.vm.provision :shell, inline: "sudo apt install -y dirmngr gnupg apt-transport-https ca-certificates software-properties-common"

  # Add MangoDB
  config.vm.provision :shell, inline: "sudo apt install -y mongodb-org"

  # Start mangodb on boot
  config.vm.provision :shell, inline: "sudo systemctl enable --now mongod"

  # Add desktop environment
  config.vm.provision :shell, inline: "sudo apt install -y --no-install-recommends ubuntu-desktop"
  config.vm.provision :shell, inline: "sudo apt install -y --no-install-recommends virtualbox-guest-dkms virtualbox-guest-utils virtualbox-guest-x11"
  
  # Add `vagrant` to Administrator
  config.vm.provision :shell, inline: "sudo usermod -a -G sudo vagrant"

  # Add Firefox
  config.vm.provision :shell, inline: "sudo apt install -y firefox"

  # Add Apache
  config.vm.provision :shell, inline: "sudo apt install -y apache2"

  # Add node.js
  config.vm.provision :shell, inline: "sudo apt install -y nodejs"

  # Restart
  config.vm.provision :shell, inline: "sudo shutdown -r now"
end
