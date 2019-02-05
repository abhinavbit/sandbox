Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/xenial64"
  config.vm.box_check_update = false
  $enable_serial_logging = false

  config.vm.define "app" do |h|
h.vm.network "private_network", ip: "192.168.135.102"
    h.vm.hostname = "standalone"

   h.vm.provision "shell" do |s|
    s.path = "init/standalone_init.sh"
    s.privileged = true
  end

    h.vm.provider "virtualbox" do |vb|
     vb.memory = "2048"
     vb.cpus = 2
    end

    h.vm.provision "file", source: "standalone.yml", destination: "/vagrant/standalone.yml"
    h.vm.provision "ansible_local" do |ansible|
    ansible.install_mode = "pip"
    ansible.playbook = "standalone.yml"
    ansible.compatibility_mode = "2.0"
  end

  end

end
