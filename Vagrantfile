Vagrant::Config.run do |config|
  #config.vm.box     = "ubuntu-precise64"
  config.vm.box     = "centos63"
  #config.vm.box_url = "http://files.vagrantup.com/precise64.box"

  config.vm.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]

  config.vm.provision :shell do |shell|
    shell.inline = "
      if type apt-get > /dev/null;then
        sudo apt-get -y update;
      # chef -> yum_helper  -> yum dump -> cause 'yum update' timeout, will break 'vagrant up'
      #elif type yum > /dev/null;then
      #  sudo yum -y update;
      fi"
  end

  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = [".."]
    chef.log_level      = :debug

    chef.add_recipe     "chef-wkhtmltopdf"

  end
end
