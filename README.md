# Description
Vagrant VM for running devstack and tempest.

# Requirements
* VirtualBox >= 4.2
* NFS Server Support

# Usage

1. Install

        $ git clone https://github.com/att-cloud/vagrant-devstack.git

1. Change directory

        $ cd vagrant-devstack

1. Initialize and update git submodules

        $ git submodule init && git submodule update

1. Install gem dependencies

        $ bundle install

1. Start virtual machine

        $ vagrant up

1. SSH to virtual machine

        $ vagrant ssh

1. Install OpenStack

        $ sudo /root/devstack/stack.sh

1. Configure tempest (optional; required if running tempest tests)

        $ /opt/stack/devstack/tools/configure_tempest.sh

1. Run tempest tests

        $ nosetests /opt/stack/tempest/tempest
