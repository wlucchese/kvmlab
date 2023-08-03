# kvmlab
ansible roles to create vms with qemu/kvm with libvirt on RHEL9
Role Name
=========

Create virtual machines (vm's) with ansible playbooks, on RHEL9, using qemu/kvm with libvirt and local .iso .qcow2 images

Requirements
------------

#to install epel repo on rhel9
sudo subscription-manager repos --enable codeready-builder-for-rhel-9-$(arch)-rpms
sudo dnf install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm

sudo dnf install qemu-kvm libvirt virt-install
#Install the necessary packages for QEMU-KVM and libvirt

sudo systemctl start libvirtd
sudo systemctl enable libvirtd
#Start and enable the libvirtd service, which manages virtualization capabilities on your system

sudo usermod -aG libvirt $(whoami)
#Add your user account to the libvirt group to allow managing virtual machines without root privileges

ansible --version
virsh --version

SSH key pair created for access to vm's

Role Defaults
--------------
Determines where your image will be pulled from.

Role Handlers
--------------
Not currently in use

Role Meta
--------------
versions of software used in playbooks

Role Tasks
--------------
Tasks used for creation of vm's

Role Templates
--------------
Templates used for creation of vm's, best to use previous VM's to get exact specifications down

Role Test
--------------
Not currently in use

Role Vars/Variables
--------------
ansible-galaxy role init kvm_provision (or which ever name you want)

- Role kvm_provision was created successfully

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------
---
- name: Deploys VM based on cloud image
  hosts: localhost
  gather_facts: yes
  become: yes
  vars:
    ansible_python_interpreter: /usr/bin/python3  # Add this line; adjust the path as necessary
    pool_dir: "/var/lib/libvirt/images"
    vm: vm-name
    vcpus: vm-cpus
    ram_mb: vm-ram
    cleanup: no
    net: default
    ssh_pub_key: "/home/user/.ssh/id_rsa.pub" #change path to ssh key storage

  tasks:
    - name: KVM Provision role
      include_role:
        name: kvm_provision
      vars:
        libvirt_pool_dir: "{{ pool_dir }}"
        vm_name: "{{ vm }}"
        vm_vcpus: "{{ vcpus }}"
        vm_ram_mb: "{{ ram_mb }}"
        vm_net: "{{ net }}"
        cleanup_tmp: "{{ cleanup }}"
        ssh_key: "{{ ssh_pub_key }}"


License
-------

BSD

Author Information
------------------

wlucchese
