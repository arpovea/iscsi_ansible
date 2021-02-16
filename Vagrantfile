Vagrant.configure("2") do |config|

  config.vm.define "nodo1" do |nodo1|
      nodo1.vm.provider "virtualbox" do |vb|
          vb.name = "nodo1"
          vb.cpus = 1
          vb.memory = 1024
         ## Añado 4 discos de 500M a la VM servidor
          vb.customize ["createmedium","disk","--filename","./tmp/disk1.vdi","--size", 500]
          vb.customize ["createmedium","disk","--filename","./tmp/disk2.vdi","--size", 500]
          vb.customize ["createmedium","disk","--filename","./tmp/disk3.vdi","--size", 500]
          vb.customize ["createmedium","disk","--filename","./tmp/disk4.vdi","--size", 500]
          vb.customize ["storagectl",:id,"--name","SATA Controller","--portcount",5]
          vb.customize ["storageattach",:id,"--storagectl","SATA Controller","--port",1,"--device",0,"--type","hdd","--hotpluggable","on","--medium","./tmp/disk1.vdi"]
          vb.customize ["storageattach",:id,"--storagectl","SATA Controller","--port",2,"--device",0,"--type","hdd","--hotpluggable","on","--medium","./tmp/disk2.vdi"]
          vb.customize ["storageattach",:id,"--storagectl","SATA Controller","--port",3,"--device",0,"--type","hdd","--hotpluggable","on","--medium","./tmp/disk3.vdi"]
          vb.customize ["storageattach",:id,"--storagectl","SATA Controller","--port",4,"--device",0,"--type","hdd","--hotpluggable","on","--medium","./tmp/disk4.vdi"]
      end

      nodo1.vm.network "private_network", ip: "192.168.50.2"
      nodo1.vm.provider :virtualbox
      nodo1.vm.box = "debian/buster64"
      nodo1.vm.hostname = "servidor-iscsi"
  end

  config.vm.define "nodo2" do |nodo2|

      nodo2.vm.provider "virtualbox" do |vb|
          vb.name = "nodo2"
          vb.cpus = 1
          vb.memory = 1024
      end

      nodo2.vm.network "private_network", ip: "192.168.50.3"
      nodo2.vm.provider :virtualbox
      nodo2.vm.box = "debian/buster64"
      nodo2.vm.hostname = "cliente-linux"

  end

  config.vm.define "nodo3" do |nodo3|
      
      nodo3.vm.provider "virtualbox" do |vb|
          vb.name = "nodo3"
          vb.cpus = 2
      end

      nodo3.vm.network "private_network", ip: "192.168.50.4"
      nodo3.vm.provider :virtualbox
      nodo3.vm.box = "senglin/win-10-enterprise-vs2015community"
      nodo3.vm.hostname = "cliente-windows"
      nodo3.winrm.username = "vagrant"
      nodo3.winrm.password = "vagrant"
      nodo3.vm.communicator = :winrm


  end

  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "site.yml"
    ansible.config_file = "ansible.cfg"

  end
end