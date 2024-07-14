# -*- mode: ruby -*-
# vi: set ft=ruby :
class VagrantPlugins::ProviderVirtualBox::Action::Network
  def dhcp_server_matches_config?(dhcp_server, config)
    true
  end
end

Vagrant.configure("2") do |config|

  # Configuración de la primera máquina virtual
  config.vm.define "web1" do |web1|
    web1.vm.box = "ubuntu/jammy64"  # Box Ubuntu 18.04 LTS
    web1.vm.hostname = "web1"
    web1.vm.network "private_network", type: "dhcp"
    web1.vm.provider "virtualbox" do |vb|
      vb.memory = "512"  # Configurar la memoria según sea necesario
      # vb.gui = true
    end

    # Provisión para instalar Apache y compartir la carpeta
    web1.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y apache2
    SHELL
  end

  # Configuración de la segunda máquina virtual (similar a la primera)
  config.vm.define "web2" do |web2|
    web2.vm.box = "ubuntu/jammy64"
    web2.vm.hostname = "web2"
    web2.vm.network "private_network", type: "dhcp"
    web2.vm.provider "virtualbox" do |vb|
      vb.memory = "512"
    end

    # Provisión para instalar Apache y compartir la carpeta
    web2.vm.provision "shell", inline: <<-SHELL
      apt-get update
      apt-get install -y apache2
    SHELL
  end

  config.vm.synced_folder "./html", "/var/www/html", type: "virtualbox"

end
