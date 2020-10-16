Vagrant.configure("2") do |config| 
  config.vm.define :infra do |main| 
    main.vm.box = "ubuntu/focal64" 
    main.vm.hostname = "infra" 
    #config.vm.network :forwarde_port, guest: 80, host: 8002 
    #config.vm.network :private_network, ip: "192.168.100.13" 
    main.vm.provider :virtualbox do |vb| 
      vb.customize ["modifyvm", :id, "--memory", "2048"] 
    end 
    config.vm.provision :chef_solo do |chef| 
      chef.log_level = :info 
      chef.roles_path = "roles" 
      chef.data_bags_path = "data_bags" 
      chef.add_role "base" 
      chef.add_role "zabbix-db" 
      chef.add_role "zabbix-server" 
      chef.add_role "graylog2" 
    end 
  end 
 
config.vm.define :vm1 do |main| 
    main.vm.box = "ubuntu/focal64" 
    main.vm.hostname = "vm1" 
    config.vm.network :forwarded_port, guest: 80, host: 8001 
    config.vm.network :private_network, ip: "192.168.100.14" 
    main.vm.provider :virtualbox do |vb| 
      vb.customize ["modifyvm", :id, "--memory", "2048"] 
    end 
    config.vm.provision :chef_solo do |chef| 
      chef.log_level = :info 
      chef.roles_path = "roles" 
      chef.data_bags_path = "data_bags" 
      chef.add_role "base" 
      chef.add_role "zabbix-client" 
      chef.add_role "projectname" 
    end 
  end 
end
