# -*- mode: ruby -*-

Vagrant.configure(2) do |config|
  config.vm.box = "generic/ubuntu1604"

  N = 3
  (1..N).each do |machine_id|
    config.vm.define "vm#{machine_id}" do |c1|
      c1.vm.hostname = "vm#{machine_id}"
      c1.vm.network "public_network", :dev => "enp2s0", :mode => 'bridge', ip: "192.168.11.#{20 + machine_id}"

      c1.vm.provider :libvirt do |domain|
        domain.memory = 2048
      end

      if machine_id == N
        c1.vm.provision "ansible" do |ansible|
          ansible.playbook = "ansible-common/provision/site.yml"
          ansible.inventory_path = "ansible-common/provision/hosts"
          ansible.limit = 'all'
        end
      end

    end
  end
end
