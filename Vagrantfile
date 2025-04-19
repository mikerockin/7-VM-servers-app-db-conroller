# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.define "controller" do |controller|
    controller.vm.box = "centos/9" 
    controller.vm.box_url="https://kojihub.stream.centos.org/kojifiles/packages/CentOS-Stream-Vagrant/9/20250326.0/images/CentOS-Stream-Vagrant-9-20250326.0.x86_64.vagrant-virtualbox.box"
    controller.vm.hostname = "controller" 
    controller.vm.network "private_network", ip: "192.168.56.15" 

    controller.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end


    controller.vm.provision "shell", inline: <<-SHELL
      sudo  dnf  -y install  nginx
    SHELL
  end

  config.vm.define "db" do |db|
    db.vm.box = "centos/9" 
    db.vm.box_url="https://kojihub.stream.centos.org/kojifiles/packages/CentOS-Stream-Vagrant/9/20250326.0/images/CentOS-Stream-Vagrant-9-20250326.0.x86_64.vagrant-virtualbox.box"
    db.vm.hostname = "db" 
    db.vm.network "private_network", ip: "192.168.56.10" 

    db.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end


    db.vm.provision "shell", inline: <<-SHELL
      curl  -L  https://dev.mysql.com/get/mysql84-community-release-el9-1.noarch.rpm  -O
      sudo  dnf  install  -y  mysql84-community-release-el9-1.noarch.rpm
      sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2023
      sudo  dnf  install  -y  mysql-server
      cat <<'END_MYSQLD' /etc/my.cnf
server-id = 2
log-bin = mysql-bin
relay-log = mysql-relay-bin
gtid_mode = ON
enforce_gtid_consistency = ON
read-only = 1

ssl_ca=/var/lib/mysql/ca.pem
ssl_cert=/var/lib/mysql/client-cert.pem
ssl_key=/var/lib/mysql/client-key.pem
END_MYSQLD
      sudo  systemctl  start  mysqld
      sudo  systemctl  enable  mysqld
      sudo  systemctl status mysqld
    SHELL
  end



  config.vm.define "db1" do |db1|
    db1.vm.box = "centos/9" 
    db1.vm.box_url="https://kojihub.stream.centos.org/kojifiles/packages/CentOS-Stream-Vagrant/9/20250326.0/images/CentOS-Stream-Vagrant-9-20250326.0.x86_64.vagrant-virtualbox.box"
    db1.vm.hostname = "db1" 
    db1.vm.network "private_network", ip: "192.168.56.11" 

    db1.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end


    db1.vm.provision "shell", inline: <<-SHELL
      curl  -L  https://dev.mysql.com/get/mysql84-community-release-el9-1.noarch.rpm  -O
      sudo  dnf  install  -y  mysql84-community-release-el9-1.noarch.rpm
      sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2023
      sudo  dnf  install  -y  mysql-server
      cat <<'END_MYSQLD' /etc/my.cnf
server-id = 2
log-bin = mysql-bin
relay-log = mysql-relay-bin
gtid_mode = ON
enforce_gtid_consistency = ON
read-only = 1

ssl_ca=/var/lib/mysql/ca.pem
ssl_cert=/var/lib/mysql/client-cert.pem
ssl_key=/var/lib/mysql/client-key.pem
END_MYSQLD
      sudo  systemctl  start  mysqld
      sudo  systemctl  enable  mysqld
      sudo  systemctl status mysqld
    SHELL
  end

  config.vm.define "db2" do |db2|
    db2.vm.box = "centos/9" 
    db2.vm.box_url="https://kojihub.stream.centos.org/kojifiles/packages/CentOS-Stream-Vagrant/9/20250326.0/images/CentOS-Stream-Vagrant-9-20250326.0.x86_64.vagrant-virtualbox.box"
    db2.vm.hostname = "db2" 
    db2.vm.network "private_network", ip: "192.168.56.12" 

    db2.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end


    db2.vm.provision "shell", inline: <<-SHELL
      curl  -L  https://dev.mysql.com/get/mysql84-community-release-el9-1.noarch.rpm  -O
      sudo  dnf  install  -y  mysql84-community-release-el9-1.noarch.rpm
      sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2023
      sudo  dnf  install  -y  mysql-server
      cat <<'END_MYSQLD' /etc/my.cnf
server-id = 3
log-bin = mysql-bin
relay-log = mysql-relay-bin
gtid_mode = ON
enforce_gtid_consistency = ON
read-only = 1

ssl_ca=/var/lib/mysql/ca.pem
ssl_cert=/var/lib/mysql/client-cert.pem
ssl_key=/var/lib/mysql/client-key.pem
END_MYSQLD
      sudo  systemctl  start  mysqld
      sudo  systemctl  enable  mysqld
      sudo  systemctl status mysqld
    SHELL
  end


  config.vm.define "web1" do |web1|
    web1.vm.box = "centos/9" 
    web1.vm.box_url="https://kojihub.stream.centos.org/kojifiles/packages/CentOS-Stream-Vagrant/9/20250326.0/images/CentOS-Stream-Vagrant-9-20250326.0.x86_64.vagrant-virtualbox.box"
    web1.vm.hostname = "web1" 
    web1.vm.network "private_network", ip: "192.168.56.20"

    web1.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end


    web1.vm.provision "shell", inline: <<-SHELL
      sudo useradd -m -s /bin/bash reguser
      echo 'reguser:regu' | sudo chpasswd
      sudo usermod -aG wheel reguser
      sudo dnf install -y https://dev.mysql.com/get/mysql80-community-release-el9-1.noarch.rpm
      sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2023
      sudo dnf -y install gcc python3-devel mysql-community-devel
      sudo  dnf  -y  install  git
      cd /home/vagrant/
      git  clone  https://github.com/app-generator/ecommerce-flask-stripe
      sudo  mv  ecommerce-flask-stripe/  /opt/ecommerce-flask-stripe/
      sudo  chown  -R  reguser:reguser  /opt/ecommerce-flask-stripe/
      sudo -u reguser bash -c '
      echo "Run as  reguser" > /home/reguser/testfile.txt
      whoami >> /home/reguser/testfile.txt
      cd  /opt/ecommerce-flask-stripe/
      pip  install  -r  requirements.txt
      cp  env.sample  .env
    '
    SHELL
  end


  config.vm.define "web2" do |web2|
    web2.vm.box = "centos/9" 
    web2.vm.box_url="https://kojihub.stream.centos.org/kojifiles/packages/CentOS-Stream-Vagrant/9/20250326.0/images/CentOS-Stream-Vagrant-9-20250326.0.x86_64.vagrant-virtualbox.box"
    web2.vm.hostname = "web2" 
    web2.vm.network "private_network", ip: "192.168.56.22"

    web2.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end


    web2.vm.provision "shell", inline: <<-SHELL
      sudo useradd -m -s /bin/bash reguser
      echo 'reguser:regu' | sudo chpasswd
      sudo usermod -aG wheel reguser
      sudo dnf install -y https://dev.mysql.com/get/mysql80-community-release-el9-1.noarch.rpm
      sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2023
      sudo dnf -y install gcc python3-devel mysql-community-devel
      sudo  dnf  -y  install  git
      cd /home/vagrant/
      git  clone  https://github.com/app-generator/ecommerce-flask-stripe
      sudo  mv  ecommerce-flask-stripe/  /opt/ecommerce-flask-stripe/
      sudo  chown  -R  reguser:reguser  /opt/ecommerce-flask-stripe/
      sudo -u reguser bash -c '
      echo "Run as  reguser" > /home/reguser/testfile.txt
      whoami >> /home/reguser/testfile.txt
      cd  /opt/ecommerce-flask-stripe/
      pip  install  -r  requirements.txt
      cp  env.sample  .env
    '
    SHELL
  end


  config.vm.define "web3" do |web3|
    web3.vm.box = "centos/9" 
    web3.vm.box_url="https://kojihub.stream.centos.org/kojifiles/packages/CentOS-Stream-Vagrant/9/20250326.0/images/CentOS-Stream-Vagrant-9-20250326.0.x86_64.vagrant-virtualbox.box"
    web3.vm.hostname = "web3" 
    web3.vm.network "private_network", ip: "192.168.56.23"

    web3.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 1
    end


    web3.vm.provision "shell", inline: <<-SHELL
      sudo useradd -m -s /bin/bash reguser
      echo 'reguser:regu' | sudo chpasswd
      sudo usermod -aG wheel reguser
      sudo dnf install -y https://dev.mysql.com/get/mysql80-community-release-el9-1.noarch.rpm
      sudo rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2023
      sudo dnf -y install gcc python3-devel mysql-community-devel
      sudo  dnf  -y  install  git
      cd /home/vagrant/
      git  clone  https://github.com/app-generator/ecommerce-flask-stripe
      sudo  mv  ecommerce-flask-stripe/  /opt/ecommerce-flask-stripe/
      sudo  chown  -R  reguser:reguser  /opt/ecommerce-flask-stripe/
      sudo -u reguser bash -c '
      echo "Run as  reguser" > /home/reguser/testfile.txt
      whoami >> /home/reguser/testfile.txt
      cd  /opt/ecommerce-flask-stripe/
      pip  install  -r  requirements.txt
      cp  env.sample  .env
    '
    SHELL
  end
end

