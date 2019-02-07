# 2018-10-13 (cc) <paul4hough@gmail.com>
#

Vagrant.configure("2") do |config|
  config.vm.box_check_update = false

  prom = "prom"

  config.vm.define prom do |bcfg|
    bcfg.vm.box         = "c7g"
    bcfg.vm.hostname    = prom
    bcfg.vm.network     'private_network', ip: '10.0.5.10'
    bcfg.vm.network     'forwarded_port', guest: 8500, host: 8500
    # bcfg.vm.network     'forwarded_port', guest: 9090, host: 9090
    # bcfg.vm.network     'forwarded_port', guest: 9093, host: 9093
    # bcfg.vm.network     "forwarded_port", guest: 8086, host: 18086
    bcfg.vm.provider 'virtualbox' do |vb|
      vb.name      = prom
      vb.cpus      = 1
      vb.memory    = 1024
      vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
      vb.customize ['modifyvm', :id, '--natdnspassdomain1', 'on']
      vb.customize ['modifyvm', :id, '--usb', 'off']
    end
    bcfg.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/node-prom.yml"
    end
  end

  anode = "anode"

  config.vm.define anode do |bcfg|
    bcfg.vm.box         = "c7g"
    bcfg.vm.hostname    = anode
    bcfg.vm.network    'private_network', ip: '10.0.5.11'
    # bcfg.vm.network "forwarded_port", guest: 3000, host: 13000
    # bcfg.vm.network "forwarded_port", guest: 8086, host: 18086
    bcfg.vm.provider 'virtualbox' do |vb|
      vb.name      = anode
      vb.cpus      = 1
      vb.memory    = 1024
      vb.customize ['modifyvm', :id, '--natdnshostresolver1', 'on']
      vb.customize ['modifyvm', :id, '--natdnspassdomain1', 'on']
      vb.customize ['modifyvm', :id, '--usb', 'off']
    end
    bcfg.vm.provision "ansible" do |ansible|
      ansible.playbook = "ansible/node-anode.yml"
    end
  end
end
