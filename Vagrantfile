nodes = [:node1, :node2, :node3]

def node_number(node)
  s = node.to_s
  s[4,s.length-4]
end

def ip1(node)
  '192.168.10.1' + node_number(node)
end

def ip2(node)
  '192.168.20.1' + node_number(node)
end

macs1 = {
  :node1 => "080027B62266",
  :node2 => "0800272AB772",
  :node3 => "08002715F8C2"
}

macs2 = {
  :node1 => "080027734393",
  :node2 => "080027E58473",
  :node3 => "080027A9374D"
}

VAGRANTFILE_API_VERSION = "2"
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define :dns do |config|
    config.vm.hostname = "dns"
    config.vm.box = "bsrk/ganeti-dns"
    config.vm.synced_folder ".", "/vagrant", disabled: true
    config.vm.network "private_network",
      ip: '192.168.10.2',
      name: ENV["N1"],
      auto_config: false,
      adapter: 2
    config.vm.network "private_network",
      ip: '192.168.20.2',
      name: ENV["N2"],
      auto_config: false,
      adapter: 3
  end
  nodes.each do |node|
    config.vm.define node do |config|
      config.vm.hostname = node.to_s
      config.vm.box = "bsrk/ganeti"
      config.vm.synced_folder ".", "/vagrant", disabled: true
      config.vm.network "private_network",
        ip: ip1(node),
        mac: macs1[node],
        name: ENV["N1"],
        auto_config: false,
        adapter: 2
      config.vm.network "private_network",
        ip: ip2(node),
        mac: macs2[node],
        name: ENV["N2"],
        auto_config: false,
        adapter: 3
    end
  end
end
