Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :box
    config.cache.enable :apt
    config.cache.enable :npm
  end

  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.cpus = 2
  end

  config.vm.network "forwarded_port", guest: 8080, host: 8080

  config.vm.define "flowgrant" do |node| end

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "vvvv"

    ansible.groups = {
      "all" => ['flowgrant'],
      "girder" => ['flowgrant'],
      "mongo" => ['flowgrant'],
      "rabbitmq" => ['flowgrant']
    }

    ansible.extra_vars = {
      default_user: "vagrant"
    }

    ansible.playbook = "devops/ansible/site.yml"
  end
end
