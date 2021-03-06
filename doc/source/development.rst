===========
Development
===========

This section describes how to set up an OpenStack controller in a virtual
machine using `Vagrant <https://www.vagrantup.com/>`_ and Kayobe.

Preparation
===========

First, ensure that Vagrant is installed and correctly configured.

Next, clone kayobe::

    git clone https://github.com/stackhpc/kayobe

Change the current directory to the kayobe repository::

    cd kayobe

Inspect kayobe's ``Vagrantfile``, noting the provisioning steps::

    less Vagrantfile

Bring up a virtual machine::

    vagrant up

Wait for the VM to boot.

Installation
============

SSH into the controller VM::

    vagrant ssh

Source the kayobe virtualenv activation script::

    source kayobe-venv/bin/activate

Change the current directory to the Vagrant shared directory::

    cd /vagrant

Source the kayobe environment file::

    source kayobe-env

Bootstrap the kayobe control host::

    kayobe control host bootstrap

Configure the controller host::

    kayobe overcloud host configure

During execution of this command, SELinux will be disabled and the VM will be
rebooted, causing you to be logged out. Wait for the VM to finish rebooting and
log in, performing the same environment setup steps as before::

    vagrant ssh
    source kayobe-venv/bin/activate
    cd /vagrant
    source kayobe-env

Run the host configuration command again to completion::

    kayobe overcloud host configure

Build container images::

    kayobe overcloud container image build

Deploy the control plane services::

    kayobe overcloud service deploy

Source the OpenStack environment file::

    source ${KOLLA_CONFIG_PATH:-/etc/kolla}/admin-openrc.sh

Perform post-deployment configuration::

    kayobe overcloud post configure

Next Steps
==========

The OpenStack control plane should now be active. Try out the following:

* register a user
* create an image
* upload an SSH keypair
* access the horizon dashboard

The cloud is your oyster!

To Do
=====

Create virtual baremetal nodes to be managed by the OpenStack control plane.
