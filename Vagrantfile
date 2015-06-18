Vagrant.configure("2") do |config|

  config.vm.define "hub0" do |master|
     master.vm.hostname = "jenkins"
     master.vm.network :forwarded_port, host: 4567, guest: 8080
     master.vm.network "private_network", ip: "172.28.128.10"
     config.vm.provision "ansible" do |ansible|
         ansible.playbook = "provisioning/ansible/playbook.yml"
         ansible.verbose = 'v'
         ansible.groups = {
         	"jenkins" => ["hub0"]
         }
     end
  end

 config.vm.provider :virtualbox do |vb, override|
     override.vm.box = "springboard/wheezy"
 end

  # This configuration is for our EC2 instance
  config.vm.provider :aws do |aws, override|
    aws.access_key_id = "AKIAJXKW27TTWDAK2GVA"
    aws.secret_access_key = "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"
    aws.region = "us-west-2"
    aws.region_config "us-west-2", :ami => "ami-ad4a069d"
    aws.keypair_name = "vagrant"
    aws.security_groups = ["launch-wizard-1" ]

    override.vm.box = "dummy"
    override.vm.box_url = "https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box"
    override.ssh.username = "ubuntu"
    override.ssh.private_key_path = "vagrant.pem"
  end
end

