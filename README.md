kvm_provision_lab
=================

With this role you can deploy a lab environment of Linux VMs to a KVM hypervisor.

Requirements
------------

This role needs the community.libvirt.virt module on the Ansible Control Node and the commands virt-customize, qemu-img and virsh on the remote host.

Role Variables
--------------

libvirt_pool_dir: "/var/lib/libvirt/images"
vm_root_pass: "123456"
ssh_key: "/path/to/ssh-pub-key"

guests:
  test:
    vm_ram_mb: 512
    vm_vcpus: 1
    vm_net: default
    os_type: rhel7
    file_type: qcow2
    base_image_name: rhel7-template
    vm_template: "rhel7-template"
    second_hdd: false
    second_hdd_size: ""
A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - kvm_provision_lab

License
-------

GPL-2.0-or-later

Author Information
------------------

Author: Tronde
