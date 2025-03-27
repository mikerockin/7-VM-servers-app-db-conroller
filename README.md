# 7-VM-servers-app-db-conroller + Scripts

### Includes:

    Vagrantfile:

    creates a web application infrastructure with load balancing and database replication on 
    CentOS 9 virtual machines.
    All VMs are configured with private IP addresses on the 192.168.56.0/24 network.
    
        controller (192.168.56.15):
    A virtual machine with Nginx installed that serves as an entry point and distributes traffic 
    between the web servers.
       
        db (192.168.56.10):
    A primary database server with MySQL 8.4 Community Server, configured as a master for 
    replication.
        
        db1 (192.168.56.11) and db2 (192.168.56.12):
    Secondary database servers with MySQL 8.4 Community Server, configured as slaves for 
    replication with db.
        
        web1 (192.168.56.20), web2 (192.168.56.22), web3 (192.168.56.23):
    Web servers where the ecommerce-flask-stripe 
    https://github.com/app-generator/ecommerce-flask-stripe 
    (Flask application is deployed, connected to the database. On each server:
    Git, Python 3, and MySQL development libraries are installed.
    The ecommerce-flask-stripe repository is cloned, dependencies are installed.

    Scripts:

    1. Install Prometheus 
    2. Install Grafana
    3. Install Prometheus Node Exporter
    4. Install Prometheus Mysqld Exporter
    5. Install Prometheus Alert Manager
    


###### Tested on CentOS Stream 9 with Vagrant ###### 
    https://kojihub.stream.centos.org/kojifiles/packages/CentOS-Stream-Vagrant/9/20250326.0/images/CentOS-Stream-Vagrant-9-20250326.0.x86_64.vagrant-virtualbox.box
