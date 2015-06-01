Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: "echo Hello"
  config.vm.box = "ubuntu/trusty64"

  config.vm.define "web" do |web|
    web.vm.network "public_network", bridge: "wlan1"
    web.vm.provider "virtualbox" do |vbxWeb|
      vbxWeb.memory = 1024
      vbxWeb.cpus = 1
    end
  
    web.vm.provision "ansible" do |ansWeb|
      ansWeb.verbose = "v"
      ansWeb.playbook = "./ansible/webservers.yml"
      ansWeb.sudo = "true"
      ansWeb.groups = { "webservers" => ["web"], "all_groups:children" => ["webservers"] }
    end
  end

  config.vm.define "test" do |test|
    test.vm.network "public_network", bridge: "wlan1"
    test.vm.provider "virtualbox" do |vbxTest, override|
      vbxTest.memory = 1024
      vbxTest.cpus = 2
    end

    test.vm.provision "ansible" do |ansTest|
      ansTest.verbose = "v"
      ansTest.sudo = true
      ansTest.playbook = "./ansible/test.yml"
      ansTest.groups = { "tests" => ["test"], "all_groups:children" => ["tests"] }
    end
  end

  config.vm.define "appx" do |appx|
    appx.vm.network "public_network", bridge: "wlan1"
    appx.vm.provider "virtualbox" do |vbxAppx, override|
      vbxAppx.memory = 1024
      vbxAppx.cpus = 2
    end

    appx.vm.provision "ansible" do |ansAppx|
      ansAppx.verbose = "v"
      ansAppx.sudo = true
      ansAppx.playbook = "./ansible/appx.yml"
      ansAppx.groups = { "g_appx" => ["appx"], }
    end
  end

  config.vm.define "db" do |db|
    db.vm.network "public_network", bridge: "wlan1"
    db.vm.provider "virtualbox" do |vbxDb, override|
      override.vm.box = "ubuntu/trusty32"
      vbxDb.memory = 1024
      vbxDb.cpus = 1
    end

    db.vm.provision "ansible" do |ansDb|
      ansDb.verbose = "v"
      ansDb.sudo = true
      ansDb.playbook = "./ansible/dbservers.yml"
      ansDb.groups = { "dbservers" => ["db"], "all_groups:children" => ["dbservers"] }
#      ansDb.sudo_user = "root"
#      ansDb.ask_sudo_pass = false
#      ansDb.extra_vars = { ansible_ssh_user: 'root' }
#      ansDb.playbook = "./ansible/db.yml"
#      ansDb.raw_arguments = "--limit @/home/klemen/default.retry"
    end
  end

end
