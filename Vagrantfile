# -*- mode: ruby -*-
# vi: set ft=ruby :

#задаём переменные с количеством машин

$dev_mach = 5
$db_mach = 2
$lamp_mach = 2

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.box_check_update = false

#Cоздаём машины для разработчиков, количество задали в переменных.
#Пул ip адресов перенесли, чтоб не пересекались с другими машинами.

   (1..$dev_mach).each do |i|
        config.vm.define "dev#i" do |dev|
         dev.vm.network  "public_network", ip: "192.168.1.#{10+i}"
         dev.vm.hostname = "dev#{i}"  
         dev.vm.provider "virtualbox" do |vb|
                vb.memory = "1096"
         end
        end
   end


#Создаём машины для баз данных.

   (1..$db_mach).each do |i|
        config.vm.define "db#i" do |db|
         db.vm.network "public_network", ip: "192.168.1.#{50+i}"
         db.vm.hostname = "db#{i}"  
         db.vm.provider "virtualbox" do |vb|
                vb.memory = "1024"
         end
        end
   end
#Создамём машину для сервера непрерывной интеграции.

 config.vm.define "ci" do |ci|
     ci.vm.network "public_network", ip: "192.168.1.60"
     ci.vm.hostname = "ci"  
     ci.vm.provider "virtualbox" do |vb|
         vb.memory = "1048"
     end
 end
#Создаём машины для разворачивания приложения

    (1..$lamp_mach).each do |i|
         config.vm.define "lamp#{i}" do |lamp|
          lamp.vm.network "public_network", ip: "192.168.1.#{150+i}"
          lamp.vm.hostname = "lamp_node#{i}"  
          lamp.vm.provider "virtualbox" do |vb|
           vb.memory = "512"
          end
         end
     end
#Создаём машину для шлюза.

 config.vm.define "gate" do |gate|
     gate.vm.network "public_network", ip: "192.168.1.2"
     gate.vm.hostname = "gate"  
     gate.vm.provider "virtualbox" do |vb|
         vb.memory = "512"
     end
 end


end