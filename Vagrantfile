VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.ssh.insert_key = false
    config.vm.box_check_update = false

    config.vm.define "vagrant1" do |vagrant1|
        vagrant1.vm.box = "bento/centos-7.1"
        vagrant1.vm.network "private_network", ip: "192.168.168.201"

        # On CentOS7, you should restart network to take effect of ip address; but you need not to do this on ubuntu-16.10
        vagrant1.vm.provision "restart-network", type: "shell", preserve_order: true, inline: "sudo systemctl restart network"
    end

    config.vm.define "vagrant2" do |vagrant2|
        vagrant2.vm.box = "bento/centos-7.1"
        vagrant2.vm.network "private_network", ip: "192.168.168.202"

        # On CentOS7, you should restart network to take effect of ip address; but you need not to do this on ubuntu-16.10
        # 如果一个config里面定义了多个provision,并且执行顺序会影响到结果,需要使用preserve_order: true让provision按照代码里给定的顺序运行。
        vagrant2.vm.provision "restart-network", type: "shell", preserve_order: true, inline: "sudo systemctl restart network"

        vagrant2.vm.provision "ansible" do |ansible|
            preserve_order = true
            ansible.limit = "all"
            ansible.verbose = "v" # "v" or "vvvv"
            ansible.playbook = "tests/test_vagrant.yml"

            ansible.groups = {
                "zookeeper" => ["vagrant[1:2]"]
            }

            ansible.host_vars = {
                "vagrant1" => {"linux_bridge_bridge_name" => "br3", "linux_bridge_device_name" => "enp0s8"},
                "vagrant2" => {"linux_bridge_bridge_name" => "br3", "linux_bridge_device_name" => "enp0s8"},
            }
        end

    end
end

