Vagrant.configure("2") do |config|
config.vm.define "k8s.master" do |master|
    master.vm.box="sbeliakou/centos"
    master.vm.hostname="k8s-master"
    master.vm.network :private_network, ip: "192.168.56.15"
    master.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.customize ["modifyvm", :id, "--cpuexecutioncap", "30"]
      vb.name = "ansible-k8s-master"
    end

  end
  config.vm.define "k8s.worker" do |worker|
    worker.vm.box="sbeliakou/centos"
    worker.vm.hostname="k8s-worker"
    worker.vm.network :private_network, ip: "192.168.56.20"
    worker.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.customize ["modifyvm", :id, "--cpuexecutioncap", "30"]
      vb.name = "ansible-k8s-worker"
    end
    worker.vm.provision :ansible do |ansible|
        ansible.limit = "all"
        ansible.playbook = "playbook.yml"
        ansible.inventory_path = "./inventory"
        ansible.raw_arguments  = [
        "--connection=paramiko"]
    end
  end
end
