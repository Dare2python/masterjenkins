# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.provider "virtualbox" do |vb|
  #   vb.gui = true
    vb.memory = "2048"
    vb.cpus = 2
  end

  config.vm.network "forwarded_port", guest: 80, host: 1080
  config.vm.network "forwarded_port", guest: 8080, host: 18080

  config.vm.provision "shell", inline: <<-SHELL
   yum -v -y install wget
   # yum -v -y install httpd wget
   # echo Welcome! > /var/www/html/index.html 
   # systemctl start httpd
   # cd /opt/
   # wget -q --no-cookies --no-check-certificate --header "Cookie: gpw_e24=http%3A%2F%2Fwww.oracle.com%2F; oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u161-b12/2f38c3b165be4555a1fa6e98c45e0808/jdk-8u161-linux-x64.tar.gz"
   # tar xzf jdk-8u161-linux-x64.tar.gz
   cd /opt/jdk1.8.0_161/
   yum -y install java-1.8.0-openjdk.x86_64
   alternatives --install /usr/bin/java java /opt/jdk1.8.0_161/bin/java 2
   alternatives --install /usr/bin/jar jar /opt/jdk1.8.0_161/bin/jar 2
   alternatives --install /usr/bin/javac javac /opt/jdk1.8.0_161/bin/javac 2
   alternatives --set jar /opt/jdk1.8.0_161/bin/jar
   alternatives --set javac /opt/jdk1.8.0_161/bin/javac
   echo "export JAVA_HOME=/opt/jdk1.8.0_161" >> /etc/environment
   echo "export JRE_HOME=/opt/jdk1.8.0_161/jre" >> /etc/environment
   echo "export PATH=$PATH:/opt/jdk1.8.0_161/bin:/opt/jdk1.8.0_161/jre/bin" >> /etc/environment
   echo "export _JAVA_OPTIONS=-Xmx512M" >> /etc/environment
   java -version
   wget -q -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
   rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
   yum -y install jenkins
   service jenkins start
   chkconfig jenkins on
   service jenkins status
   service firewalld start
   firewall-cmd --zone=public --add-port=8080/tcp --permanent
   firewall-cmd --zone=public --add-service=http --permanent
   firewall-cmd --reload
   firewall-cmd --list-all
   cat /var/lib/jenkins/secrets/initialAdminPassword
   date
   echo Done! 
  SHELL
end
