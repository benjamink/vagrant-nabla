# -*- mode: ruby -*-
# vi: set ft=ruby :

# Version of Go to install
golang_ver="1.11.2"

Vagrant.configure("2") do |config|
  config.vm.hostname = "nabla"
  config.vm.box = "ubuntu/bionic64"

  config.vm.synced_folder "gosrc", "/home/vagrant/go/src"

  config.vm.provision "shell", inline: <<-SCRIPT
    echo "SCRIPT: Installing Docker"
    if ! docker --version 2>/dev/null
    then
      export APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=True
      export DEBIAN_FRONTEND=noninteractive
      apt-get update
      apt-get -y install apt-transport-https ca-certificates curl software-properties-common
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
      apt-key fingerprint 0EBFCD88
      add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
      apt-get update
      apt-get -y install docker-ce
    fi
  SCRIPT

  config.vm.provision "shell", inline: <<-SCRIPT
    echo "SCRIPT: Installing Go"
    if ! go version 2>/dev/null
    then
      curl -fsSL -o /tmp/go.tar.gz https://dl.google.com/go/go#{golang_ver}.linux-amd64.tar.gz
      tar -C /usr/local -xzf /tmp/go.tar.gz
      echo "export PATH=$PATH:/usr/local/go/bin" >> /etc/profile
      rm -f /tmp/go.tar.gz
      echo "export GOPATH=/home/vagrant/go" >> /home/vagrant/.profile
    fi
  SCRIPT

end
