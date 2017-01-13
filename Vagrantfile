# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

	# SSH options.
	#config.ssh.insert_key = false
	config.ssh.insert_key = true
	config.ssh.forward_agent = true

	config.vm.provider :virtualbox do |vb|
		vb.customize ["modifyvm", :id, "--memory", "1024"]
	end

	config.vm.define "jekyll_201701" do |worker|
		worker.vm.box = "ubuntu/xenial64"
		worker.vm.network :forwarded_port, guest: 4000, host: 4000
		worker.vm.synced_folder ".", "/vagrant"
		worker.vm.provision :shell do |sh|
			sh.privileged = false 
			sh.inline = <<-SCRIPT
				# TODO: Locales
				# Timezone
				sudo timedatectl set-timezone CET
				# TODO: NTP daemon
				# TODO: SSH server
				# TODO: Firewall (ufw)
				# Install Jekyll
				sudo apt-get -y install jekyll
				jekyll serve -w -s /vagrant -d /vagrant/_site --host=0.0.0.0 --detach
			SCRIPT
		end
	end

end

