# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure(2) do |config|
  config.vm.define :control do |control_config|
    control_config.vm.box = "ubuntu/trusty64"
    control_config.vm.hostname = 'control'
    control_config.vm.network :private_network, ip: '10.0.15.10'
    control_config.vm.provider 'virtualbox' do |vb|
      vb.memory = '256'
    end
    config.vm.synced_folder 'src/', '/home/vagrant/ansible/'
    control_config.vm.provision :ansible do |ansible|
      ansible.playbook = 'env/control.yml'
    end
  end

  (1..2).each do |i|
    config.vm.define "app0#{i}" do |app|
      app.vm.box = 'ubuntu/trusty64'
      app.vm.hostname = "app0#{i}"
      app.vm.network :private_network, ip: "10.0.15.2#{i}"
      app.vm.network 'forwarded_port', guest: 80, host: "808#{i}"

      app.vm.provider 'virtualbox' do |vb|
        vb.memory = '256'
      end
      app.vm.provision :ansible do |ansible|
        ansible.playbook = 'env/other.yml'
      end
    end
  end

  config.vm.define :db do |db_config|
    db_config.vm.box = "ubuntu/trusty64"
    db_config.vm.hostname = 'db01'
    db_config.vm.network :private_network, ip: '10.0.15.30'
    db_config.vm.provider 'virtualbox' do |vb|
      vb.memory = '512'
    end
    db_config.vm.provision :ansible do |ansible|
      ansible.playbook = 'env/other.yml'
    end
  end

  config.vm.define :lb do |lb_config|
    lb_config.vm.box = "ubuntu/trusty64"
    lb_config.vm.hostname = 'lb01'
    lb_config.vm.network :private_network, ip: '10.0.15.11'
    lb_config.vm.network 'forwarded_port', guest: 80, host: 8080
    lb_config.vm.provider 'virtualbox' do |vb|
      vb.memory = '256'
    end
    lb_config.vm.provision :ansible do |ansible|
      ansible.playbook = 'env/other.yml'
    end
  end
end
