CLUSTER_SIZE = 3

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  (1..CLUSTER_SIZE).each do |box_id|
    config.vm.define "galera-db-#{box_id}" do |box|
      box.vm.hostname = "galera-db-#{box_id}"
      box.vm.network "private_network", ip: "192.168.121.#{200+box_id}"

      if box_id == CLUSTER_SIZE
        box.vm.provision :ansible do |ansible|
          ansible.limit = "all"
          ansible.become = true
          ansible.playbook = "galera.yml"
          ansible.groups = {
            "galera_cluster" => ["galera-db-1", "galera-db-2", "galera-db-3"]
          }
        end
      end
    end
  end
end
