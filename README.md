# Welcome to **stackinabox.io**

## Introduction

This Vagrant project will stand up a single Ubuntu 14.04 VM running OpenStack and Docker using VirtualBox. The project will pull Docker images for [UrbanCode Deploy](https://hub.docker.com/r/stackinabox/urbancode-deploy/), [UrbanCode Deploy Agent](https://hub.docker.com/r/stackinabox/urbancode-deploy-agent/), [UrbanCode Patterns Blueprint Designer](https://hub.docker.com/r/stackinabox/urbancode-patterns-designer/), and [UrbanCode Patterns Engine](https://hub.docker.com/r/stackinabox/urbancode-patterns-engine/).  Using this Vagrant project, once running using `vagrant up`, you'll be able to design and develop OpenStack Heat-based cloud automation that you can use to deploy applications to the embedded [OpenStack](https://www.blueboxcloud.com/) cloud or to any other cloud provider supported by [UrbanCode Deploy's Blueprint Designer](https://developer.ibm.com/urbancode/products/urbancode-deploy/features/blueprint-designer/) ([Amazon Web Services](https://aws.amazon.com/), [SoftLayer](http://www.softlayer.com/), [Azure](https://azure.microsoft.com/), or even your on-premise [VMware vCenter](https://www.vmware.com/products/vcenter-server)).

Using this Vagrant project, our hope is that you will share the automation that you develop to deploy applications to the cloud with the larger community.  For an example check out [JKE Banking Application](https://github.com/stackinabox/jke)

## Future Integrations

It's planned to add further Docker images to this vagrant setup to support many other deployment automation tools such as:  

  - [UrbanCode Build](https://developer.ibm.com/urbancode/products/urbancode-build/) (not yet implemented)
  - [UrbanCode Release](https://developer.ibm.com/urbancode/products/urbancode-release/) (not yet implemented)
  - [Chef Server](https://www.chef.io/chef/) (not yet implemented)
  - [Salt Stack](https://saltstack.com/) (not yet implemented)
  - [Puppet](https://puppet.com/) (not yet implemented)

### Setup Instructions

##### Download and install these tools  

  - [Oracle VirtualBox](https://www.virtualbox.org/wiki/Downloads)  
  - [Vagrant](https://www.vagrantup.com/downloads.html)
  - [Git](https://git-scm.com/) 

##### Install required Vagrant plugins  
````
vagrant plugin install vagrant-docker-compose
vagrant plugin install vagrant-multi-hostsupdater
```

### Running `vagrant up`
Verify that VirtualBox, Vagrant, and Git are installed and running by typing `vboxmanage help`, `vagrant help`, and `git help` at the command shell.  

Execute these commands:
````
git clone https://github.com/stackinabox/stackinabox.io.git 
cd stackinabox.io/vagrant
vagrant up
```

The `vagrant up` command will take a while to complete.  The project will download the OPDK (Open Patterns Development Kit) VirtualBox VM from atlas.hashicorp.com. Once downloaded, Vagrant will launch the VM in VirtualBox in "headless" mode (no GUI).  When the VM is up, Docker Compose is used to start the UrbanCode products in multiple containers.  The Vagrant project will also set several entries in your machine's `hosts` file, and this step may prompt for a password.  Ultimately you will see this output at the end of process, which is the result of running `docker-compose up`.

````
....
==> opdk: Creating ucddb
==> opdk: Creating heatengine
==> opdk: Creating blueprintdb
==> opdk: Creating ucd
==> opdk: Creating blueprintdesigner
==> opdk: Creating agent
==> opdk: Creating agent-relay
....
```

After the Vagrant machine is up, you can open your local web browser to the [Blueprint Designer](http://designer.stackinabox.io:9080/lanscaper) and login with `demo`/`labstack`.  The demo user is intended to be the primary user for building your automation.  The demo user belongs to a 'demo' team in the Blueprint Designer and has it's own tenant in the embedded [OpenStack](http://bluebox.stackinabox.io).  Additional login information is provided below.

### Access Information
[OPDK Web Terminal](http://192.168.27.100:4200/) - Available at http://192.168.27.100:4200/
- username: vagrant
- password: vagrant

OpenStack i.e. [BlueBox](http://openstack.stackinabox.io) - Available at http://openstack.stackinabox.io 
- username: demo
- password: labstack  
_____________________  
- username: admin
- password: labstack
	 
[UrbanCode Deploy Server](http://ucd.stackinabox.io:8080) - Available at http://ucd.stackinabox.io:8080
- username: admin
- password: admin

[UrbanCode Deploy Blueprint Designer](http://designer.stackinabox.io:9080/landscaper) (Heat Orchestration Template Designer) - Available at http://designer.stackinabox.io:9080/landscaper
- username: demo
- password: labstack  
_____________________  
- username: ucdpadmin
- password: ucdpadmin
		 
[UrbanCode Deploy Heat Engine](http://heat.stackinabox.io:8004) - Verify at http://heat.stackinabox.io:8004

### Install the JKE Sample
Open your browser to the ["OPDK web terminal"](http://192.168.27.100:4200/).  Login and execute the following commands:
````
git clone https://github.com/stackinabox/jke.git /vagrant/patterns/jke
cd /vagrant/patterns/jke
./init.sh
```

Open your browser to the [JKE Tutorial](http://designer.stackinabox.io:9080/landscaper/view/tutorial) and login with `demo`/`labstack`.  You will see a "Guided Tour" frame on the right side of the browser window.  Follow the instructions which will guide you on how to deploy the JKE sample using UrbanCode Deploy and Blueprint Designer.

### Halt, Resume, or Destroy the Vagrant machine
You can run `vagrant global-status` to see a list of running Vagrant machines and their IDs.

To halt/suspend a machine, naviagte to the directory where you cloned the stackinabox.io repository and execute `vagrant halt`:
````
cd /path/to/stackinabox.io/repo
vagrant halt
```

To resume a halted machine and restore all previous work/data:
````
cd /path/to/stackinabox.io/repo
vagrant resume
```

To destroy a Vagrant machine and restart with a clean slate:
````
cd /path/to/stackinabox.io/repo
vagrant destroy <vagrant-env-id>
vagrant up
```

### Connect the Blueprint Designer to AWS
Open your browser to the ["OPDK web terminal"](http://192.168.27.100:4200/), login, and execute `~/aws-setup.sh`.  Then follow the instructions at the end of the script execution.
