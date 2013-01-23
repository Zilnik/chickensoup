# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|
  config.vm.box = "precise64"
  config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/app", "1"]
  config.vm.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]

  config.vm.network :hostonly, "192.168.33.10"

  config.vm.forward_port 80, 8080
  config.vm.forward_port 3333, 3334

  config.vm.provision :shell, :path => "scripts/node_globals.sh"

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = '..\..\cookbooks'
    chef.add_recipe("nodejs")
    chef.add_recipe("nodejs::npm")

    chef.add_recipe("git")
  end
end
