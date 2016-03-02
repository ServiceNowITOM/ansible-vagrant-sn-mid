# -*- mode: ruby -*-
# vi: set ft=ruby :

# Set our default provider for this Vagrantfile to 'vmware_appcatalyst'
ENV['VAGRANT_DEFAULT_PROVIDER'] = 'vmware_appcatalyst'

nodes = [
	{ hostname: 'now-mid-01', box: 'hashicorp/precise64' },
	{ hostname: 'now-vmn-01', box: 'hashicorp/precise64' }
]


Vagrant.configure(2) do |config|

	# 1 CPU, 384GB Memory
	config.vm.provider 'vmware_appcatalyst' do |v|
		v.cpus = '1'
		v.memory = '384'
	end
	
	nodes.each do |node|
		config.vm.define node[:hostname] do |node_config|
			node_config.vm.box = node[:box]
			node_config.vm.hostname = node[:hostname]
		end
    end
    
    # Ansible playbook to setup mid and vm nodes
    config.vm.provision :ansible do |ansible|
    	ansible.playbook = "provision/site.yml"
    	ansible.groups = {
    		"mids"  => [ 'now-mid-01' ],
    		"nodes" => [ 'now-vmn-01' ]
    	}
    end
end