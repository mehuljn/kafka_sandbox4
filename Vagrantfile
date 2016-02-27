# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

  if Vagrant.has_plugin?("vagrant-cachier")
    config.cache.scope = :machine
  end

#  config.vm.provider "virtualbox" do |vb|
#    vb.customize ["modifyvm", :id, "--natnet1", "10.30.3.0/24"]
#  end

#Prefer to start Zookeeper and Kafka nodes manually
#Start Zookeeper with 
#bin/zookeeper-server-start.sh config/zookeeper.properties > /dev/null 2>&1 &
#Start Kafka With
#bin/kafka-server-start.sh config/server.properties >/dev/null 2>&1 &

  config.vm.define "kafkamaster1" do |kafkamaster1|
    kafkamaster1.vm.box = "relativkreativ/centos-7-minimal"
    kafkamaster1.vm.hostname = "kafkamaster1"
    kafkamaster1.vm.network :public_network, bridge: "en0: Wi-Fi (AirPort)", ip: "10.30.3.11"
    kafkamaster1.vm.network "forwarded_port", guest: 9092, host: 19092
    kafkamaster1.vm.network "forwarded_port", guest: 2181, host: 12181 
    kafkamaster1.vm.provision "shell", inline: <<-SHELL
     sudo yum install -y java-1.7.0-openjdk*
     sudo cp -p /vagrant/kafka_2.11-0.9.0.0.tgz /home/vagrant/.
     sudo service firewalld stop
     cd /home/vagrant
     tar -xvf kafka_2.11-0.9.0.0.tgz
     echo "initLimit=5" >> kafka_2.11-0.9.0.0/config/zookeeper.properties 
     echo "syncLimit=2" >> kafka_2.11-0.9.0.0/config/zookeeper.properties 
     echo "server.1=10.30.3.11:2888:3888" >> kafka_2.11-0.9.0.0/config/zookeeper.properties 
     echo "server.2=10.30.3.12:2888:3888" >> kafka_2.11-0.9.0.0/config/zookeeper.properties 
     echo "server.3=10.30.3.13:2888:3888" >> kafka_2.11-0.9.0.0/config/zookeeper.properties
     mkdir -p /tmp/zookeeper
     echo 1 > /tmp/zookeeper/myid
     sed -i 's/broker\.id=0/broker\.id=1/g' kafka_2.11-0.9.0.0/config/server.properties
     sed -i 's/zookeeper\.connect=localhost:2181/zookeeper\.connect=10.30.3.11:2181,10.30.3.12:2181,10.30.3.13:2181/g' kafka_2.11-0.9.0.0/config/server.properties 
    SHELL
  end 
 
  config.vm.define "kafkamaster2" do |kafkamaster2|
    kafkamaster2.vm.box = "relativkreativ/centos-7-minimal"
    kafkamaster2.vm.hostname = "kafkamaster2"
    kafkamaster2.vm.network :public_network, bridge: "en0: Wi-Fi (AirPort)", ip: "10.30.3.12" 
    kafkamaster2.vm.network "forwarded_port", guest: 9092, host: 29092
    kafkamaster2.vm.network "forwarded_port", guest: 2181, host: 22181 
    kafkamaster2.vm.provision "shell", inline: <<-SHELL
     sudo yum install -y java-1.7.0-openjdk*
     sudo cp -p /vagrant/kafka* /home/vagrant/.
     sudo service firewalld stop
     cd /home/vagrant
     tar -xvf kafka_2.11-0.9.0.0.tgz
     echo "initLimit=5" >> kafka_2.11-0.9.0.0/config/zookeeper.properties 
     echo "syncLimit=2" >> kafka_2.11-0.9.0.0/config/zookeeper.properties 
     echo "server.1=10.30.3.11:2888:3888" >> kafka_2.11-0.9.0.0/config/zookeeper.properties 
     echo "server.2=10.30.3.12:2888:3888" >> kafka_2.11-0.9.0.0/config/zookeeper.properties 
     echo "server.3=10.30.3.13:2888:3888" >> kafka_2.11-0.9.0.0/config/zookeeper.properties
     mkdir -p /tmp/zookeeper
     echo 2 > /tmp/zookeeper/myid 
     sed -i 's/broker\.id=0/broker\.id=2/g' kafka_2.11-0.9.0.0/config/server.properties
     sed -i 's/zookeeper\.connect=localhost:2181/zookeeper\.connect=10.30.3.11:2181,10.30.3.12:2181,10.30.3.13:2181/g' kafka_2.11-0.9.0.0/config/server.properties 
    SHELL
  end
 
  config.vm.define "kafkamaster3" do |kafkamaster3|
    kafkamaster3.vm.box = "relativkreativ/centos-7-minimal"
    kafkamaster3.vm.hostname = "kafkamaster3" 
    kafkamaster3.vm.network :public_network, bridge: "en0: Wi-Fi (AirPort)", ip: "10.30.3.13"
    kafkamaster3.vm.network "forwarded_port", guest: 9092, host: 39092
    kafkamaster3.vm.network "forwarded_port", guest: 2181, host: 32181 
    kafkamaster3.vm.provision "shell", inline: <<-SHELL
     sudo yum install -y java-1.7.0-openjdk*
     sudo cp -p /vagrant/kafka* /home/vagrant/.
     sudo service firewalld stop
     cd /home/vagrant
     tar -xvf kafka_2.11-0.9.0.0.tgz
     echo "initLimit=5" >> kafka_2.11-0.9.0.0/config/zookeeper.properties 
     echo "syncLimit=2" >> kafka_2.11-0.9.0.0/config/zookeeper.properties 
     echo "server.1=10.30.3.11:2888:3888" >> kafka_2.11-0.9.0.0/config/zookeeper.properties 
     echo "server.2=10.30.3.12:2888:3888" >> kafka_2.11-0.9.0.0/config/zookeeper.properties 
     echo "server.3=10.30.3.13:2888:3888" >> kafka_2.11-0.9.0.0/config/zookeeper.properties
     mkdir -p /tmp/zookeeper
     echo 3 > /tmp/zookeeper/myid 
     sed -i 's/broker\.id=0/broker\.id=3/g' kafka_2.11-0.9.0.0/config/server.properties
     sed -i 's/zookeeper\.connect=localhost:2181/zookeeper\.connect=10.30.3.11:2181,10.30.3.12:2181,10.30.3.13:2181/g' kafka_2.11-0.9.0.0/config/server.properties 
    SHELL

  end


end
