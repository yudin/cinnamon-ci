Vagrant.configure("2") do |config|

  config.vm.define "hub0" do |master|
     master.vm.box = "springboard/wheezy"
     master.vm.hostname = "jenkins"
     master.vm.network :forwarded_port, host: 4567, guest: 8080
#     master.vm.network :forwarded_port, host: 4567, guest: 4444
     master.vm.network "private_network", ip: "172.28.128.10"
     config.vm.provision "ansible" do |ansible|
         ansible.playbook = "provisioning/ansible/playbook.yml"
         ansible.verbose = 'vvvv'
         ansible.groups = {
         	"jenkins" => ["hub0"]
         }
     end
  end

end

