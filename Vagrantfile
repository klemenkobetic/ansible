Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: "echo Hello"
  config.vm.box = "ubuntu/trusty64"

  config.vm.define "web" do |web|
    web.vm.provider "virtualbox" do |vbxWeb|
      vbxWeb.memory = 1024
      vbxWeb.cpus = 2
    end
  
    web.vm.provision "ansible" do |ansWeb|
#      ansWeb.verbose = "vvvv"
      ansWeb.playbook = "./ansible/web.yml"
    end
  end

  config.vm.define "db" do |db|
    db.vm.provider "virtualbox" do |vbxDb, override|
      override.vm.box = "ubuntu/trusty32"
      vbxDb.memory = 1024
      vbxDb.cpus = 2
    end

    db.vm.provision "ansible" do |ansDb|
#      ansDb.verbose = "v"
#      ansDb.playbook = "./ansible/db.yml"
      ansDb.playbook = "./ansible/default.yml"
    end
  end
end
