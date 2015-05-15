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
      ansWeb.playbook = "./ansible/webservers.yml"
      ansWeb.groups = { "webservers" => ["web"], "all_groups:children" => ["webservers"] }
    end
  end

  config.vm.define "db" do |db|
    db.vm.provider "virtualbox" do |vbxDb, override|
      override.vm.box = "ubuntu/trusty32"
      vbxDb.memory = 1024
      vbxDb.cpus = 2
    end

    db.vm.provision "ansible" do |ansDb|
      ansDb.verbose = "v"
      ansDb.sudo = true
#      ansDb.sudo_user = "root"
#      ansDb.ask_sudo_pass = false
      ansDb.playbook = "./ansible/dbservers.yml"
      ansDb.groups = { "dbservers" => ["db"], "all_groups:children" => ["dbservers"] }

#      ansDb.extra_vars = { ansible_ssh_user: 'root' }
#      ansDb.playbook = "./ansible/db.yml"
#      ansDb.raw_arguments = "--limit @/home/klemen/default.retry"
    end
  end
end
