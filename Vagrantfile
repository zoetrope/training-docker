# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64"
  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 2
  end
  config.vm.provision "shell", inline: <<-SHELL
    apt-get update
    apt-get install -y --no-install-recommends apt-transport-https ca-certificates curl software-properties-common jq build-essential tree

    # setup docker
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    apt-get update
    apt-get install -y docker-ce
    usermod -aG docker vagrant

    # setup docker-compose
    curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose

    # setup golang
    snap install go --classic
    cat <<EOF >> /home/vagrant/.bashrc
export GOPATH=/home/vagrant/go
export PATH=$PATH:/usr/local/go/bin:$GOPATH/bin
export GO111MODULE=on
EOF

  SHELL
end
