kvm_provision_lab
=================

With this role you can deploy a lab environment of Linux VMs to a KVM/QEMU hypervisor.

For the hypervisor host I have tested but other/newer releases might work too:

 - Debian 11
 - RHEL 9
 - Fedora 37

If you are capable of reading German you'll find a tutorial on my blog at: https://www.my-it-brain.de/wordpress/labor-umgebung-mit-ansible-in-kvm-erstellen/.

Requirements
------------

This role needs the community.libvirt.virt module on the Ansible Control Node and the commands virt-customize, qemu-img and virsh on the remote host.

You can use the command `ansible-galaxy collection install community.libvirt` to install the collection to your Ansible Control Node. For the commands needed on the remote host, please use the package manager of your distribution to install them.

Role Variables
--------------

The following code block shows the variables you can set. You need to specify the directory where the disk images for your guest domains are going to be created using `libvirt_pool_dir`. With `vm_root_pass` you set the password for the root user and add an ssh-key to the authorized_keys file by setting `ssh_key`.

The VMs are defined as a dictionary as shown below.

```
libvirt_pool_dir: "/var/lib/libvirt/images"
vm_root_pass: "123456"
ssh_key: "/path/to/ssh-pub-key"

guests:
  test:
    vm_ram_mb: 512
    vm_vcpus: 1
    vm_iftype: network
    vm_net: default
    os_type: rhel7
    file_type: qcow2
    base_image_name: rhel7-template
    vm_template: "rhel7-template"
    second_hdd: false
    second_hdd_size: ""
  test2:
    vm_ram_mb: 512
    vm_vcpus: 1
    vm_iftype: network
    vm_net: default
    os_type: rhel8
    file_type: qcow2
    base_image_name: rhel8-template
    vm_template: "rhel8-template"
    second_hdd: true
    second_hdd_size: "100M"
```

With the varialbes from the code block above you would create the two VMs _test_ and _test2_ with the parameters specified in the dictionary. The variables are explained in the table below.

| Variable | Description |
| --- | --- |
| `guests` | Name of the dictionary specifying the parameters for guest domains (VMs). |
| `test` | This key is used as name for the domain (VM) to create. |
| `vm_ram_mb` | Guest memory in MB. |
| `vm_vcpus` | Count of vCPU for the domain. |
| `vm_iftype` | Type of network to connect to. Possible vaules are `network` (default) or `bridge`. |
| `vm_net` | Network Name. Must already exist in your environment. |
| `os_type` | Type of the guest domain, e.g. `rhel8`, `rhel9` or `debian11`. |
| `file_type` | Defaults to qcow2. You usually don't have to change this. |
| `base_image_name` | The name of the qcow2 image that is used as the source to copy. |
| `vm_template` | Name of the template without he .xml.j2 part. |
| `second_hdd` | Boolean to specify whether a second disk image is needed or not. |
| `second_hdd_size` | Size of the second disk image. Size can be specified in k or K (kilobyte, 1024) M (megabyte,  1024k) and G (gigabyte, 1024M) and T (terabyte, 1024G). |

Dependencies
------------

- community.libvirt

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - kvm_provision_lab

Contribution
------------

In case you need additional information on how to use this role, please raise an issue with your question at: https://github.com/Tronde/kvm_provision_lab/issues
Pull requests improving this README as well as the role are appreciated.

License
-------

GPL-2.0-or-later

Author Information
------------------

Author: Tronde
