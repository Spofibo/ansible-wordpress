# -*- mode: ruby -*-
# vi: set ft=ruby :

require 'getoptlong'

opts = GetoptLong.new(
    [ '--env', GetoptLong::OPTIONAL_ARGUMENT ],
    [ '--tags', GetoptLong::OPTIONAL_ARGUMENT ],
    [ '--verbose', GetoptLong::OPTIONAL_ARGUMENT ],
    [ '--ssh-port', GetoptLong::OPTIONAL_ARGUMENT ],
)

env = 'prod'
sites = [
    {
      "db_host": "mysql.com",
      "db_name": "wp_1_db",
      "db_password": "mock",
      "db_port": 3306,
      "db_username": "wp_1_u",
      "project": "alpha",
      "url": "alpa.com"
    },
    {
      "db_host": "mysql.com",
      "db_name": "wp_2_db",
      "db_password": "mock",
      "db_port": 3306,
      "db_username": "wp_2_u",
      "project": "beta",
      "url": "beta.com"
    }
]
tags = 'all'
verbose = ''
ssh_port = ''

opts.ordering=(GetoptLong::REQUIRE_ORDER) ### this line avoids having errors when using Vagrant native arguments, i.e.: --debug

opts.each do |opt, arg|
    case opt
    when '--tags'
        tags=arg
    when '--verbose'
        verbose=arg
    when '--ssh-port'
        ssh_port=arg
    end
end

Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/focal64"

    unless ssh_port.strip.empty?
        config.vm.network "forwarded_port", id: "ssh2", guest: ssh_port, host: ssh_port
        config.ssh.port = ssh_port
    end

    config.vm.define "virtualbox" do |virtualbox|
        virtualbox.vm.hostname = "test-box"
        # virtualbox.vm.network :private_network, ip: "172.16.3.2"

        config.vm.provider :virtualbox do |v|
            v.gui = false
            v.memory = 512
            v.cpus = 1
            v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
            v.customize ["modifyvm", :id, "--ioapic", "on"]
        end

        config.vm.provision "ansible", run: "always" do |ansible|
            ansible.become = true
            ansible.ask_become_pass = false

            ansible.tags = tags
            ansible.verbose = verbose

            ansible.extra_vars = {
                env: env,
                sites: sites
            }

            ansible.playbook = "playbook.yaml"
        end
    end
end
