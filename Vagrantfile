Vagrant.configure("2") do |config|
  # Base VM OS configuration.
  config.vm.box = "debian/bookworm64"
  config.vm.provider :virtualbox do |v|
    v.memory = 1512
    v.cpus = 1
  end

  # Define two VMs with static private IP addresses.
  boxes = [
    { :name => "mysqlsrs",
      :ip => "192.168.57.10",
    },
    { :name => "mysqlrep",
      :ip => "192.168.57.15",
    }
  ]
  # Provision each of the VMs.
  boxes.each do |opts|
    config.vm.define opts[:name] do |config|
      config.vm.hostname = opts[:name]
      config.vm.network "private_network", ip: opts[:ip]

      # Provision with Ansible for each machine
      config.vm.provision "ansible" do |ansible|
        ansible.playbook = "provisioning/playbook.yml"  # Путь к общему playbook
        ansible.inventory_path = "provisioning/inventory.ini"  # Путь к инвентарному файлу
        ansible.become = true  # Если нужны привилегии суперпользователя
      end
    end
  end
end
