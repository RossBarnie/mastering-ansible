The repo I used to follow along with the Mastering Ansible course on Udemy.

Setup and Requirements
====

The idea behind this environment setup (see `env/` and the `Vagrantfile`) is
that I have an OSX machine, and I want to run the control machine, database,
loadbalancer and application servers as Vagrant VMs, each provisioned by
ansible.

With that in mind you will need:

- ansible
- Vagrant

Starting the VMs
===

`vagrant up` should take care of setting up the networking, provisioning and
boot of your VMs.

Once they are up, ssh into the control machine using `vagrant ssh control` and
change directory to `/home/vagrant/ansible`.
This is where you will spend the majority of your time, and where the rest of
these commands should be run.

Configuring Ansible Vault
===

Before running any playbooks you will need to configure the ansible vault
password like so:

`echo demo >> ~/.vault_pass.txt`

Configuring SSH
===

Generate an ssh key (github has some documentation on this).

Run `ansible-playbook playbooks/ssh-addkeys.yml --ask-pass` and enter
'vagrant' when prompted for a password.
This will add the newly-generated ssh key to all of our hosts.

Main playbook
===

Run `ansible-playbook site.yml`.

This is the main playbook which will set up the database, loadbalancer and
demo app and their dependencies.
It will take some time.

Verification
===

Run `ansible-playbook playbooks/stack_status.yml` and if it's all green then
you've successfully created the finished product.

