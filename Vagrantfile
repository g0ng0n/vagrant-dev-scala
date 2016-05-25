# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

$script = <<SCRIPT
apt-get -y update
apt-get -y upgrade
apt-get -y autoremove
apt-get -f install
apt-get install -y python-software-properties debconf-utils
add-apt-repository -y ppa:webupd8team/java
apt-get update
echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | sudo debconf-set-selections
apt-get install -y oracle-java8-installer
apt-get -y autoremove

wget http://www.scala-lang.org/files/archive/scala-2.11.8.deb
dpkg -i scala-2.11.8.deb
apt-get -y update
apt-get -y -f install scala

wget http://dl.bintray.com/sbt/debian/sbt-0.13.9.deb
dpkg -i sbt-0.13.9.deb
apt-get -y update
apt-get -y -f install sbt

SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.define "scala", primary: true do |scala|
        scala.vm.box = "ubuntu/trusty64"
        scala.vm.provision "shell", inline: $script
    end

    config.vm.provider "virtualbox" do |vb|
        vb.memory = 2048
		vb.gui = true
        vb.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
    end
end
