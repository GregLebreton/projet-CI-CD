Vagrant.configure("2") do |config|

    # Linux OS CentOS
    config.vm.box = "geerlingguy/centos7"
    #config.vm.network "public_network"

    # JENKINS MASTER
    config.vm.define "jenkins" do |jenkins|
        jenkins.vm.hostname = "jenkins"
        # static ip address
        jenkins.vm.network :private_network, ip: "192.168.60.2", bridge: "wlp5s0"
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/jenkins.yml"
        end
    end

    # DOCKER SLAVE JENKINS
    config.vm.define "docker" do |docker|
        docker.vm.hostname = "docker"
        # static ip address
        docker.vm.network :private_network, ip: "192.168.60.3", bridge: "wlp5s0"
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/docker.yml"
        end
    end

    # NEXUS
    config.vm.define "nexus" do |nexus|
        nexus.vm.hostname = "nexus"
        # static ip address
        nexus.vm.network :private_network, ip: "192.168.60.4", bridge: "wlp5s0"
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/nexus.yml"
        end
    end

    # KUBERNETES + TERRAFORM
    # config.vm.provider :virtualbox do |v|
    #   v.memory = 1024
    #   v.cpus = 1
    #   v.linked_clone = true
    #   end
    # # config.vm.define "kube" do |kube|
    # # Define three VMs with static private IP addresses.
    # boxes = [
    #     { :name => "kube1", :ip => "192.168.33.71" },
    #     { :name => "kube2", :ip => "192.168.33.72" },
    #     { :name => "kube3", :ip => "192.168.33.73" }
    # ]

    # # Provision each of the VMs.
    # boxes.each do |opts|
    #     config.vm.define opts[:name] do |config|
    #     config.vm.hostname = opts[:name]
    #     config.vm.network :private_network, ip: opts[:ip], bridge: "wlp5s0"

    #     # Provision all the VMs in parallel using Ansible after last VM is up.
    #     if opts[:name] == "kube3"
    #         config.vm.provision "ansible" do |ansible|
    #         # ansible.compatibility_mode = "2.0"
    #         ansible.playbook = "ansible/kubernetes.yml"
    #         ansible.limit = "all"
    #         # ansible.become = true
    #         ansible.groups = {
    #             "kubernetes" => ["kube1", "kube2", "kube3"],
    #             "kubernetes_master" => ["kube1"],
    #             "kubernetes_master:vars" => {
    #             kubernetes_role: "master",
    #             swapfile_path: "/dev/mapper/vagrant--vg-swap_1",
    #             kubernetes_apiserver_advertise_address: "192.168.33.71"
    #             },
    #             "kubernetes_node" => ["kube2", "kube3"],
    #             "kubernetes_node:vars" => {
    #             kubernetes_role: "node",
    #             swapfile_path: "/dev/mapper/vagrant--vg-swap_1"
    #             }
    #         }
    #             end
    #         end
    #     end
    # end 
    config.vm.define "kube" do |kube|
        kube.vm.hostname = "kube"
        kube.vm.network :private_network, ip: "192.168.60.5"
    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/kubernetes.yml"
        end
    end
end
