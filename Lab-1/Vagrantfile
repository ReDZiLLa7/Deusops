Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"

  # Number of required machines
  SERVERS = 5
  # Name of the network interface for bridge networking
  BRIDGE = "Intel(R) Wi-Fi 6 AX201 160MHz"
  
  # Define the master node
  MASTER_NODE = "srv1"

  def create_host(config, hostname, ip, is_master = false)
    config.vm.define hostname do |host|
      host.vm.network "private_network", ip: ip
      host.vm.network "public_network", bridge: BRIDGE
      host.vm.hostname = hostname
      host.vm.provider "virtualbox" do |vb|
        vb.memory = 1024  # 1GB of RAM
        vb.cpus = 1      # 1 CPU
      end

      # Common provisioning: Update and install necessary packages
      host.vm.provision "shell", inline: <<-SHELL
        apt-get update
        apt-get install -y python3-minimal openssh-server sshpass
      SHELL

      # Master node specific provisioning: generate SSH keys and distribute
      if is_master
        host.vm.provision "shell", inline: <<-SHELL
          # Generate SSH keypair if it doesn't already exist
          if [ ! -f /home/vagrant/.ssh/id_rsa ]; then
            ssh-keygen -t rsa -f /home/vagrant/.ssh/id_rsa -q -N ""
          fi

          # Copy the public key to each of the other nodes
          for i in {2..#{SERVERS}}; do
            sshpass -p 'vagrant' ssh-copy-id -o StrictHostKeyChecking=no vagrant@192.168.56.$((200 + i))
          done
        SHELL
      else
        # On all non-master nodes, prepare to accept SSH connections from master
        host.vm.provision "shell", inline: <<-SHELL
          # Ensure .ssh directory exists and has correct permissions
          mkdir -p /home/vagrant/.ssh
          chmod 700 /home/vagrant/.ssh

          # Create an authorized_keys file if it doesn't exist
          touch /home/vagrant/.ssh/authorized_keys
          chmod 600 /home/vagrant/.ssh/authorized_keys
        SHELL
      end

      yield host if block_given?
    end
  end

  # Create master node (srv1)
  create_host(config, MASTER_NODE, "192.168.56.201", true)

  # Create the other nodes (srv2 to srv5)
  (2..SERVERS).each do |machine_id|
    create_host(config, "srv#{machine_id}", "192.168.56.#{200 + machine_id}")
  end
end