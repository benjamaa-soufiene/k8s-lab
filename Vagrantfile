Vagrant.require_version ">= 2.0.0"

boxes = [
    {
        :name => "k8smaster",
        :eth1 => "192.168.20.10",
        :mem => "2048",
        :cpu => "2"
    },
    {
        :name => "k8snode1",
        :eth1 => "192.168.20.11",
        :mem => "2048",
        :cpu => "2"
    },
    {
        :name => "k8snode2",
        :eth1 => "192.168.20.12",
        :mem => "2048",
        :cpu => "2"
    }

]

Vagrant.configure(2) do |config|
  config.vm.box = "generic/ubuntu2004"

  boxes.each do |opts|
      config.vm.define opts[:name] do |config|
        config.vm.hostname = opts[:name]

        config.vm.provider "vmware_fusion" do |v|
          v.vmx["memsize"] = opts[:mem]
          v.vmx["numvcpus"] = opts[:cpu]
        end

        config.vm.provider "virtualbox" do |v|
          v.customize ["modifyvm", :id, "--memory", opts[:mem]]
          v.customize ["modifyvm", :id, "--cpus", opts[:cpu]]
        end
        config.vm.network :private_network, ip: opts[:eth1]
      end
  end
end
