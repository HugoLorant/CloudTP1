# CloudTP1 Hugo LORANT

## Prérequis
 - Le fichier Rocky-8.4-x86_64-minimal.iso doit etre present dans le dossier CloudTP1
 - Ansible doit être installé
 - La Collection ansible-collection-ansible-posix doit être installé sur la machine hôte : dnf install ansible-collection-ansible-posix -y

## Lancer le build
Pour lancer le build, il faut utiliser la commande suivante dans le répertoire TP1Repo
```
packer build rocky-8.pkr.hcl
```

## Exemple d'éxécution
```
[root@template TP1Repo]# packer build rocky-8.pkr.hcl
qemu.example: output will be in this color.

==> qemu.example: Retrieving ISO
==> qemu.example: Trying ./Rocky-8.4-x86_64-minimal.iso
==> qemu.example: Trying ./Rocky-8.4-x86_64-minimal.iso?checksum=sha256%3A0de5f12eba93e00fefc06cdb0aa4389a0972a4212977362ea18bde46a1a1aa4f
==> qemu.example: ./Rocky-8.4-x86_64-minimal.iso?checksum=sha256%3A0de5f12eba93e00fefc06cdb0aa4389a0972a4212977362ea18bde46a1a1aa4f => /root/TP1Repo/Rocky-8.4-x86_64-minimal.iso
==> qemu.example: Starting HTTP server on port 8601
==> qemu.example: Found port for communicator (SSH, WinRM, etc): 3664.
==> qemu.example: Looking for available port between 5900 and 6000 on 127.0.0.1
==> qemu.example: Starting VM, booting from CD-ROM
    qemu.example: The VM will be run headless, without a GUI. If you want to
    qemu.example: view the screen of the VM, connect via VNC without a password to
    qemu.example: vnc://127.0.0.1:5916
==> qemu.example: Waiting 10s for boot...
==> qemu.example: Connecting to VM via VNC (127.0.0.1:5916)
==> qemu.example: Typing the boot command over VNC...
    qemu.example: Not using a NetBridge -- skipping StepWaitGuestAddress
==> qemu.example: Using SSH communicator to connect: 127.0.0.1
==> qemu.example: Waiting for SSH to become available...
==> qemu.example: Connected to SSH!
==> qemu.example: Provisioning with Ansible...
    qemu.example: Setting up proxy adapter for Ansible....
==> qemu.example: Executing Ansible: ansible-playbook -e packer_build_name="example" -e packer_builder_type=qemu -e packer_http_addr=10.0.2.2:8601 --ssh-extra-args '-o IdentitiesOnly=yes' -e ansible_ssh_private_key_file=/tmp/ansible-key732987455 -i /tmp/packer-provisioner-ansible1079752414 /root/TP1Repo/playbook.yaml
    qemu.example:
    qemu.example: PLAY [all] *********************************************************************
    qemu.example:
    qemu.example: TASK [Gathering Facts] *********************************************************
    qemu.example: ok: [default]
    qemu.example:
    qemu.example: TASK [Installation des packages git make & go] *********************************
    qemu.example: changed: [default]
    qemu.example:
    qemu.example: TASK [pull du repo golang] *****************************************************
    qemu.example: changed: [default]
    qemu.example:
    qemu.example: TASK [Make golang-myip] ********************************************************
    qemu.example: changed: [default]
    qemu.example:
    qemu.example: TASK [Creation du ficher golang-myip.service] **********************************
    qemu.example: changed: [default]
    qemu.example:
    qemu.example: TASK [Ajout du contenu du service] *********************************************
    qemu.example: changed: [default]
    qemu.example:
    qemu.example: TASK [copie du service golang-myip] ********************************************
    qemu.example: changed: [default]
    qemu.example:
    qemu.example: TASK [autorisatisation SElinux pour le service] ********************************
    qemu.example: changed: [default]
    qemu.example:
    qemu.example: TASK [reload du daemon systemd] ************************************************
    qemu.example: changed: [default]
    qemu.example:
    qemu.example: TASK [enable du service golang-myip] *******************************************
    qemu.example: changed: [default]
    qemu.example:
    qemu.example: TASK [demarrage du service golang-myip] ****************************************
    qemu.example: changed: [default]
    qemu.example:
    qemu.example: TASK [Ajout cles publiques pour Bastien Balaud] ********************************
    qemu.example: changed: [default]
    qemu.example:
    qemu.example: PLAY RECAP *********************************************************************
    qemu.example: default                    : ok=12   changed=11   unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
    qemu.example:
==> qemu.example: Gracefully halting virtual machine...
==> qemu.example: Converting hard drive...
Build 'qemu.example' finished after 22 minutes 41 seconds.
```

## Exemple d'observabilité de la VM
```
TASK [Observabilitée de l'état de la VM] ***************************************
    qemu.example: ok: [default] => {
    qemu.example:     "ansible_facts": {
    qemu.example:         "all_ipv4_addresses": [
    qemu.example:             "10.0.2.15"
    qemu.example:         ],
    qemu.example:         "all_ipv6_addresses": [
    qemu.example:             "fec0::5054:ff:fe12:3456",
    qemu.example:             "fe80::5054:ff:fe12:3456"
    qemu.example:         ],
    qemu.example:         "ansible_local": {},
    qemu.example:         "apparmor": {
    qemu.example:             "status": "disabled"
    qemu.example:         },
    qemu.example:         "architecture": "x86_64",
    qemu.example:         "bios_date": "04/01/2014",
    qemu.example:         "bios_version": "1.13.0-2.module+el8.4.0+534+4680a14e",
    qemu.example:         "cmdline": {
    qemu.example:             "BOOT_IMAGE": "(hd0,msdos1)/vmlinuz-4.18.0-305.3.1.el8_4.x86_64",
    qemu.example:             "crashkernel": "auto",
    qemu.example:             "rd.lvm.lv": "rl_template/swap",
    qemu.example:             "resume": "/dev/mapper/rl_template-swap",
    qemu.example:             "ro": true,
    qemu.example:             "root": "/dev/mapper/rl_template-root"
    qemu.example:         },
    qemu.example:         "date_time": {
    qemu.example:             "date": "2021-12-14",
    qemu.example:             "day": "14",
    qemu.example:             "epoch": "1639503294",
    qemu.example:             "hour": "18",
    qemu.example:             "iso8601": "2021-12-14T17:34:54Z",
    qemu.example:             "iso8601_basic": "20211214T183454476796",
    qemu.example:             "iso8601_basic_short": "20211214T183454",
    qemu.example:             "iso8601_micro": "2021-12-14T17:34:54.476796Z",
    qemu.example:             "minute": "34",
    qemu.example:             "month": "12",
    qemu.example:             "second": "54",
    qemu.example:             "time": "18:34:54",
    qemu.example:             "tz": "CET",
    qemu.example:             "tz_offset": "+0100",
    qemu.example:             "weekday": "mardi",
    qemu.example:             "weekday_number": "2",
    qemu.example:             "weeknumber": "50",
    qemu.example:             "year": "2021"
    qemu.example:         },
    qemu.example:         "default_ipv4": {
    qemu.example:             "address": "10.0.2.15",
    qemu.example:             "alias": "ens3",
    qemu.example:             "broadcast": "10.0.2.255",
    qemu.example:             "gateway": "10.0.2.2",
    qemu.example:             "interface": "ens3",
    qemu.example:             "macaddress": "52:54:00:12:34:56",
    qemu.example:             "mtu": 1500,
    qemu.example:             "netmask": "255.255.255.0",
    qemu.example:             "network": "10.0.2.0",
    qemu.example:             "type": "ether"
    qemu.example:         },
    qemu.example:         "default_ipv6": {
    qemu.example:             "address": "fec0::5054:ff:fe12:3456",
    qemu.example:             "gateway": "fe80::2",
    qemu.example:             "interface": "ens3",
    qemu.example:             "macaddress": "52:54:00:12:34:56",
    qemu.example:             "mtu": 1500,
    qemu.example:             "prefix": "64",
    qemu.example:             "scope": "site",
    qemu.example:             "type": "ether"
    qemu.example:         },
    qemu.example:         "device_links": {
    qemu.example:             "ids": {
    qemu.example:                 "dm-0": [
    qemu.example:                     "dm-name-rl_template-root",
    qemu.example:                     "dm-uuid-LVM-IrNlkjxLKamgylyzwCpf4OWBTzszwJrZnRt6zvjsTnMy7nc9Zh13noc4l7DPYk2L"
    qemu.example:                 ],
    qemu.example:                 "dm-1": [
    qemu.example:                     "dm-name-rl_template-swap",
    qemu.example:                     "dm-uuid-LVM-IrNlkjxLKamgylyzwCpf4OWBTzszwJrZl32M7N8U7iy4rS6Dz0Hi0lYi1grLwI3J"
    qemu.example:                 ],
    qemu.example:                 "sr0": [
    qemu.example:                     "ata-QEMU_DVD-ROM_QM00001"
    qemu.example:                 ],
    qemu.example:                 "sr1": [
    qemu.example:                     "ata-QEMU_DVD-ROM_QM00003"
    qemu.example:                 ],
    qemu.example:                 "vda2": [
    qemu.example:                     "lvm-pv-uuid-wAAYJB-qFeD-NsVy-ElIE-TIdS-R99v-N4RKc0"
    qemu.example:                 ]
    qemu.example:             },
    qemu.example:             "labels": {
    qemu.example:                 "sr0": [
    qemu.example:                     "Rocky-8-4-x86_64-dvd"
    qemu.example:                 ]
    qemu.example:             },
    qemu.example:             "masters": {
    qemu.example:                 "vda2": [
    qemu.example:                     "dm-0",
    qemu.example:                     "dm-1"
    qemu.example:                 ]
    qemu.example:             },
    qemu.example:             "uuids": {
    qemu.example:                 "dm-0": [
    qemu.example:                     "047e9572-16be-4de2-a90d-907461abdc89"
    qemu.example:                 ],
    qemu.example:                 "dm-1": [
    qemu.example:                     "bc36d6f2-e3f0-4242-8fe2-933a3b09d582"
    qemu.example:                 ],
    qemu.example:                 "sr0": [
    qemu.example:                     "2021-06-20-16-15-27-00"
    qemu.example:                 ],
    qemu.example:                 "vda1": [
    qemu.example:                     "fc3e82af-aa80-4325-92c8-05ae2724ddd7"
    qemu.example:                 ]
    qemu.example:             }
    qemu.example:         },
    qemu.example:         "devices": {
    qemu.example:             "dm-0": {
    qemu.example:                 "holders": [],
    qemu.example:                 "host": "",
    qemu.example:                 "links": {
    qemu.example:                     "ids": [
    qemu.example:                         "dm-name-rl_template-root",
    qemu.example:                         "dm-uuid-LVM-IrNlkjxLKamgylyzwCpf4OWBTzszwJrZnRt6zvjsTnMy7nc9Zh13noc4l7DPYk2L"
    qemu.example:                     ],
    qemu.example:                     "labels": [],
    qemu.example:                     "masters": [],
    qemu.example:                     "uuids": [
    qemu.example:                         "047e9572-16be-4de2-a90d-907461abdc89"
    qemu.example:                     ]
    qemu.example:                 },
    qemu.example:                 "model": null,
    qemu.example:                 "partitions": {},
    qemu.example:                 "removable": "0",
    qemu.example:                 "rotational": "1",
    qemu.example:                 "sas_address": null,
    qemu.example:                 "sas_device_handle": null,
    qemu.example:                 "scheduler_mode": "",
    qemu.example:                 "sectors": "7110656",
    qemu.example:                 "sectorsize": "512",
    qemu.example:                 "size": "3.39 GB",
    qemu.example:                 "support_discard": "0",
    qemu.example:                 "vendor": null,
    qemu.example:                 "virtual": 1
    qemu.example:             },
    qemu.example:             "dm-1": {
    qemu.example:                 "holders": [],
    qemu.example:                 "host": "",
    qemu.example:                 "links": {
    qemu.example:                     "ids": [
    qemu.example:                         "dm-name-rl_template-swap",
    qemu.example:                         "dm-uuid-LVM-IrNlkjxLKamgylyzwCpf4OWBTzszwJrZl32M7N8U7iy4rS6Dz0Hi0lYi1grLwI3J"
    qemu.example:                     ],
    qemu.example:                     "labels": [],
    qemu.example:                     "masters": [],
    qemu.example:                     "uuids": [
    qemu.example:                         "bc36d6f2-e3f0-4242-8fe2-933a3b09d582"
    qemu.example:                     ]
    qemu.example:                 },
    qemu.example:                 "model": null,
    qemu.example:                 "partitions": {},
    qemu.example:                 "removable": "0",
    qemu.example:                 "rotational": "1",
    qemu.example:                 "sas_address": null,
    qemu.example:                 "sas_device_handle": null,
    qemu.example:                 "scheduler_mode": "",
    qemu.example:                 "sectors": "1024000",
    qemu.example:                 "sectorsize": "512",
    qemu.example:                 "size": "500.00 MB",
    qemu.example:                 "support_discard": "0",
    qemu.example:                 "vendor": null,
    qemu.example:                 "virtual": 1
    qemu.example:             },
    qemu.example:             "sr0": {
    qemu.example:                 "holders": [],
    qemu.example:                 "host": "IDE interface: Intel Corporation 82371SB PIIX3 IDE [Natoma/Triton II]",
    qemu.example:                 "links": {
    qemu.example:                     "ids": [
    qemu.example:                         "ata-QEMU_DVD-ROM_QM00001"
    qemu.example:                     ],
    qemu.example:                     "labels": [
    qemu.example:                         "Rocky-8-4-x86_64-dvd"
    qemu.example:                     ],
    qemu.example:                     "masters": [],
    qemu.example:                     "uuids": [
    qemu.example:                         "2021-06-20-16-15-27-00"
    qemu.example:                     ]
    qemu.example:                 },
    qemu.example:                 "model": "QEMU DVD-ROM",
    qemu.example:                 "partitions": {},
    qemu.example:                 "removable": "1",
    qemu.example:                 "rotational": "1",
    qemu.example:                 "sas_address": null,
    qemu.example:                 "sas_device_handle": null,
    qemu.example:                 "scheduler_mode": "mq-deadline",
    qemu.example:                 "sectors": "3868672",
    qemu.example:                 "sectorsize": "2048",
    qemu.example:                 "size": "1.84 GB",
    qemu.example:                 "support_discard": "0",
    qemu.example:                 "vendor": "QEMU",
    qemu.example:                 "virtual": 1
    qemu.example:             },
    qemu.example:             "sr1": {
    qemu.example:                 "holders": [],
    qemu.example:                 "host": "IDE interface: Intel Corporation 82371SB PIIX3 IDE [Natoma/Triton II]",
    qemu.example:                 "links": {
    qemu.example:                     "ids": [
    qemu.example:                         "ata-QEMU_DVD-ROM_QM00003"
    qemu.example:                     ],
    qemu.example:                     "labels": [],
    qemu.example:                     "masters": [],
    qemu.example:                     "uuids": []
    qemu.example:                 },
    qemu.example:                 "model": "QEMU DVD-ROM",
    qemu.example:                 "partitions": {},
    qemu.example:                 "removable": "1",
    qemu.example:                 "rotational": "1",
    qemu.example:                 "sas_address": null,
    qemu.example:                 "sas_device_handle": null,
    qemu.example:                 "scheduler_mode": "mq-deadline",
    qemu.example:                 "sectors": "2097151",
    qemu.example:                 "sectorsize": "512",
    qemu.example:                 "size": "1024.00 MB",
    qemu.example:                 "support_discard": "0",
    qemu.example:                 "vendor": "QEMU",
    qemu.example:                 "virtual": 1
    qemu.example:             },
    qemu.example:             "vda": {
    qemu.example:                 "holders": [],
    qemu.example:                 "host": "SCSI storage controller: Red Hat, Inc. Virtio block device",
    qemu.example:                 "links": {
    qemu.example:                     "ids": [],
    qemu.example:                     "labels": [],
    qemu.example:                     "masters": [],
    qemu.example:                     "uuids": []
    qemu.example:                 },
    qemu.example:                 "model": null,
    qemu.example:                 "partitions": {
    qemu.example:                     "vda1": {
    qemu.example:                         "holders": [],
    qemu.example:                         "links": {
    qemu.example:                             "ids": [],
    qemu.example:                             "labels": [],
    qemu.example:                             "masters": [],
    qemu.example:                             "uuids": [
    qemu.example:                                 "fc3e82af-aa80-4325-92c8-05ae2724ddd7"
    qemu.example:                             ]
    qemu.example:                         },
    qemu.example:                         "sectors": "2097152",
    qemu.example:                         "sectorsize": 512,
    qemu.example:                         "size": "1.00 GB",
    qemu.example:                         "start": "2048",
    qemu.example:                         "uuid": "fc3e82af-aa80-4325-92c8-05ae2724ddd7"
    qemu.example:                     },
    qemu.example:                     "vda2": {
    qemu.example:                         "holders": [
    qemu.example:                             "rl_template-swap",
    qemu.example:                             "rl_template-root"
    qemu.example:                         ],
    qemu.example:                         "links": {
    qemu.example:                             "ids": [
    qemu.example:                                 "lvm-pv-uuid-wAAYJB-qFeD-NsVy-ElIE-TIdS-R99v-N4RKc0"
    qemu.example:                             ],
    qemu.example:                             "labels": [],
    qemu.example:                             "masters": [
    qemu.example:                                 "dm-0",
    qemu.example:                                 "dm-1"
    qemu.example:                             ],
    qemu.example:                             "uuids": []
    qemu.example:                         },
    qemu.example:                         "sectors": "8140800",
    qemu.example:                         "sectorsize": 512,
    qemu.example:                         "size": "3.88 GB",
    qemu.example:                         "start": "2099200",
    qemu.example:                         "uuid": null
    qemu.example:                     }
    qemu.example:                 },
    qemu.example:                 "removable": "0",
    qemu.example:                 "rotational": "1",
    qemu.example:                 "sas_address": null,
    qemu.example:                 "sas_device_handle": null,
    qemu.example:                 "scheduler_mode": "mq-deadline",
    qemu.example:                 "sectors": "10240000",
    qemu.example:                 "sectorsize": "512",
    qemu.example:                 "size": "4.88 GB",
    qemu.example:                 "support_discard": "0",
    qemu.example:                 "vendor": "0x1af4",
    qemu.example:                 "virtual": 1
    qemu.example:             }
    qemu.example:         },
    qemu.example:         "discovered_interpreter_python": "/usr/libexec/platform-python",
    qemu.example:         "distribution": "Rocky",
    qemu.example:         "distribution_file_parsed": true,
    qemu.example:         "distribution_file_path": "/etc/redhat-release",
    qemu.example:         "distribution_file_variety": "RedHat",
    qemu.example:         "distribution_major_version": "8",
    qemu.example:         "distribution_release": "Green Obsidian",
    qemu.example:         "distribution_version": "8.4",
    qemu.example:         "dns": {
    qemu.example:             "nameservers": [
    qemu.example:                 "10.0.2.3"
    qemu.example:             ]
    qemu.example:         },
    qemu.example:         "domain": "",
    qemu.example:         "effective_group_id": 0,
    qemu.example:         "effective_user_id": 0,
    qemu.example:         "ens3": {
    qemu.example:             "active": true,
    qemu.example:             "device": "ens3",
    qemu.example:             "features": {
    qemu.example:                 "esp_hw_offload": "off [fixed]",
    qemu.example:                 "esp_tx_csum_hw_offload": "off [fixed]",
    qemu.example:                 "fcoe_mtu": "off [fixed]",
    qemu.example:                 "generic_receive_offload": "on",
    qemu.example:                 "generic_segmentation_offload": "off [requested on]",
    qemu.example:                 "highdma": "on [fixed]",
    qemu.example:                 "hw_tc_offload": "off [fixed]",
    qemu.example:                 "l2_fwd_offload": "off [fixed]",
    qemu.example:                 "large_receive_offload": "off [fixed]",
    qemu.example:                 "loopback": "off [fixed]",
    qemu.example:                 "netns_local": "off [fixed]",
    qemu.example:                 "ntuple_filters": "off [fixed]",
    qemu.example:                 "receive_hashing": "off [fixed]",
    qemu.example:                 "rx_all": "off [fixed]",
    qemu.example:                 "rx_checksumming": "off [fixed]",
    qemu.example:                 "rx_fcs": "off [fixed]",
    qemu.example:                 "rx_gro_hw": "off [fixed]",
    qemu.example:                 "rx_gro_list": "off",
    qemu.example:                 "rx_udp_tunnel_port_offload": "off [fixed]",
    qemu.example:                 "rx_vlan_filter": "on [fixed]",
    qemu.example:                 "rx_vlan_offload": "off [fixed]",
    qemu.example:                 "rx_vlan_stag_filter": "off [fixed]",
    qemu.example:                 "rx_vlan_stag_hw_parse": "off [fixed]",
    qemu.example:                 "scatter_gather": "off",
    qemu.example:                 "tcp_segmentation_offload": "off",
    qemu.example:                 "tls_hw_record": "off [fixed]",
    qemu.example:                 "tls_hw_rx_offload": "off [fixed]",
    qemu.example:                 "tls_hw_tx_offload": "off [fixed]",
    qemu.example:                 "tx_checksum_fcoe_crc": "off [fixed]",
    qemu.example:                 "tx_checksum_ip_generic": "off [fixed]",
    qemu.example:                 "tx_checksum_ipv4": "off [fixed]",
    qemu.example:                 "tx_checksum_ipv6": "off [fixed]",
    qemu.example:                 "tx_checksum_sctp": "off [fixed]",
    qemu.example:                 "tx_checksumming": "off",
    qemu.example:                 "tx_esp_segmentation": "off [fixed]",
    qemu.example:                 "tx_fcoe_segmentation": "off [fixed]",
    qemu.example:                 "tx_gre_csum_segmentation": "off [fixed]",
    qemu.example:                 "tx_gre_segmentation": "off [fixed]",
    qemu.example:                 "tx_gso_list": "off [fixed]",
    qemu.example:                 "tx_gso_partial": "off [fixed]",
    qemu.example:                 "tx_gso_robust": "off [fixed]",
    qemu.example:                 "tx_ipxip4_segmentation": "off [fixed]",
    qemu.example:                 "tx_ipxip6_segmentation": "off [fixed]",
    qemu.example:                 "tx_lockless": "off [fixed]",
    qemu.example:                 "tx_nocache_copy": "off",
    qemu.example:                 "tx_scatter_gather": "off [fixed]",
    qemu.example:                 "tx_scatter_gather_fraglist": "off [fixed]",
    qemu.example:                 "tx_sctp_segmentation": "off [fixed]",
    qemu.example:                 "tx_tcp6_segmentation": "off [fixed]",
    qemu.example:                 "tx_tcp_ecn_segmentation": "off [fixed]",
    qemu.example:                 "tx_tcp_mangleid_segmentation": "off [fixed]",
    qemu.example:                 "tx_tcp_segmentation": "off [fixed]",
    qemu.example:                 "tx_tunnel_remcsum_segmentation": "off [fixed]",
    qemu.example:                 "tx_udp_segmentation": "off [fixed]",
    qemu.example:                 "tx_udp_tnl_csum_segmentation": "off [fixed]",
    qemu.example:                 "tx_udp_tnl_segmentation": "off [fixed]",
    qemu.example:                 "tx_vlan_offload": "off [fixed]",
    qemu.example:                 "tx_vlan_stag_hw_insert": "off [fixed]",
    qemu.example:                 "vlan_challenged": "off [fixed]"
    qemu.example:             },
    qemu.example:             "hw_timestamp_filters": [],
    qemu.example:             "ipv4": {
    qemu.example:                 "address": "10.0.2.15",
    qemu.example:                 "broadcast": "10.0.2.255",
    qemu.example:                 "netmask": "255.255.255.0",
    qemu.example:                 "network": "10.0.2.0"
    qemu.example:             },
    qemu.example:             "ipv6": [
    qemu.example:                 {
    qemu.example:                     "address": "fec0::5054:ff:fe12:3456",
    qemu.example:                     "prefix": "64",
    qemu.example:                     "scope": "site"
    qemu.example:                 },
    qemu.example:                 {
    qemu.example:                     "address": "fe80::5054:ff:fe12:3456",
    qemu.example:                     "prefix": "64",
    qemu.example:                     "scope": "link"
    qemu.example:                 }
    qemu.example:             ],
    qemu.example:             "macaddress": "52:54:00:12:34:56",
    qemu.example:             "module": "virtio_net",
    qemu.example:             "mtu": 1500,
    qemu.example:             "pciid": "virtio0",
    qemu.example:             "promisc": false,
    qemu.example:             "speed": -1,
    qemu.example:             "timestamping": [],
    qemu.example:             "type": "ether"
    qemu.example:         },
    qemu.example:         "env": {
    qemu.example:             "DBUS_SESSION_BUS_ADDRESS": "unix:path=/run/user/0/bus",
    qemu.example:             "HOME": "/root",
    qemu.example:             "LANG": "fr_FR.UTF-8",
    qemu.example:             "LESSOPEN": "||/usr/bin/lesspipe.sh %s",
    qemu.example:             "LOGNAME": "root",
    qemu.example:             "PATH": "/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin",
    qemu.example:             "PWD": "/root",
    qemu.example:             "SELINUX_LEVEL_REQUESTED": "",
    qemu.example:             "SELINUX_ROLE_REQUESTED": "",
    qemu.example:             "SELINUX_USE_CURRENT_RANGE": "",
    qemu.example:             "SHELL": "/bin/bash",
    qemu.example:             "SHLVL": "2",
    qemu.example:             "SSH_CLIENT": "10.0.2.2 44946 22",
    qemu.example:             "SSH_CONNECTION": "10.0.2.2 44946 10.0.2.15 22",
    qemu.example:             "USER": "root",
    qemu.example:             "XDG_RUNTIME_DIR": "/run/user/0",
    qemu.example:             "XDG_SESSION_ID": "1",
    qemu.example:             "_": "/usr/libexec/platform-python"
    qemu.example:         },
    qemu.example:         "fibre_channel_wwn": [],
    qemu.example:         "fips": false,
    qemu.example:         "form_factor": "Other",
    qemu.example:         "fqdn": "template",
    qemu.example:         "gather_subset": [
    qemu.example:             "all"
    qemu.example:         ],
    qemu.example:         "hostname": "template",
    qemu.example:         "hostnqn": "",
    qemu.example:         "interfaces": [
    qemu.example:             "lo",
    qemu.example:             "ens3"
    qemu.example:         ],
    qemu.example:         "is_chroot": false,
    qemu.example:         "iscsi_iqn": "",
    qemu.example:         "kernel": "4.18.0-305.3.1.el8_4.x86_64",
    qemu.example:         "kernel_version": "#1 SMP Thu Jun 17 07:52:48 UTC 2021",
    qemu.example:         "lo": {
    qemu.example:             "active": true,
    qemu.example:             "device": "lo",
    qemu.example:             "features": {
    qemu.example:                 "esp_hw_offload": "off [fixed]",
    qemu.example:                 "esp_tx_csum_hw_offload": "off [fixed]",
    qemu.example:                 "fcoe_mtu": "off [fixed]",
    qemu.example:                 "generic_receive_offload": "on",
    qemu.example:                 "generic_segmentation_offload": "on",
    qemu.example:                 "highdma": "on [fixed]",
    qemu.example:                 "hw_tc_offload": "off [fixed]",
    qemu.example:                 "l2_fwd_offload": "off [fixed]",
    qemu.example:                 "large_receive_offload": "off [fixed]",
    qemu.example:                 "loopback": "on [fixed]",
    qemu.example:                 "netns_local": "on [fixed]",
    qemu.example:                 "ntuple_filters": "off [fixed]",
    qemu.example:                 "receive_hashing": "off [fixed]",
    qemu.example:                 "rx_all": "off [fixed]",
    qemu.example:                 "rx_checksumming": "on [fixed]",
    qemu.example:                 "rx_fcs": "off [fixed]",
    qemu.example:                 "rx_gro_hw": "off [fixed]",
    qemu.example:                 "rx_gro_list": "off",
    qemu.example:                 "rx_udp_tunnel_port_offload": "off [fixed]",
    qemu.example:                 "rx_vlan_filter": "off [fixed]",
    qemu.example:                 "rx_vlan_offload": "off [fixed]",
    qemu.example:                 "rx_vlan_stag_filter": "off [fixed]",
    qemu.example:                 "rx_vlan_stag_hw_parse": "off [fixed]",
    qemu.example:                 "scatter_gather": "on",
    qemu.example:                 "tcp_segmentation_offload": "on",
    qemu.example:                 "tls_hw_record": "off [fixed]",
    qemu.example:                 "tls_hw_rx_offload": "off [fixed]",
    qemu.example:                 "tls_hw_tx_offload": "off [fixed]",
    qemu.example:                 "tx_checksum_fcoe_crc": "off [fixed]",
    qemu.example:                 "tx_checksum_ip_generic": "on [fixed]",
    qemu.example:                 "tx_checksum_ipv4": "off [fixed]",
    qemu.example:                 "tx_checksum_ipv6": "off [fixed]",
    qemu.example:                 "tx_checksum_sctp": "on [fixed]",
    qemu.example:                 "tx_checksumming": "on",
    qemu.example:                 "tx_esp_segmentation": "off [fixed]",
    qemu.example:                 "tx_fcoe_segmentation": "off [fixed]",
    qemu.example:                 "tx_gre_csum_segmentation": "off [fixed]",
    qemu.example:                 "tx_gre_segmentation": "off [fixed]",
    qemu.example:                 "tx_gso_list": "off [fixed]",
    qemu.example:                 "tx_gso_partial": "off [fixed]",
    qemu.example:                 "tx_gso_robust": "off [fixed]",
    qemu.example:                 "tx_ipxip4_segmentation": "off [fixed]",
    qemu.example:                 "tx_ipxip6_segmentation": "off [fixed]",
    qemu.example:                 "tx_lockless": "on [fixed]",
    qemu.example:                 "tx_nocache_copy": "off [fixed]",
    qemu.example:                 "tx_scatter_gather": "on [fixed]",
    qemu.example:                 "tx_scatter_gather_fraglist": "on [fixed]",
    qemu.example:                 "tx_sctp_segmentation": "on",
    qemu.example:                 "tx_tcp6_segmentation": "on",
    qemu.example:                 "tx_tcp_ecn_segmentation": "on",
    qemu.example:                 "tx_tcp_mangleid_segmentation": "on",
    qemu.example:                 "tx_tcp_segmentation": "on",
    qemu.example:                 "tx_tunnel_remcsum_segmentation": "off [fixed]",
    qemu.example:                 "tx_udp_segmentation": "off [fixed]",
    qemu.example:                 "tx_udp_tnl_csum_segmentation": "off [fixed]",
    qemu.example:                 "tx_udp_tnl_segmentation": "off [fixed]",
    qemu.example:                 "tx_vlan_offload": "off [fixed]",
    qemu.example:                 "tx_vlan_stag_hw_insert": "off [fixed]",
    qemu.example:                 "vlan_challenged": "on [fixed]"
    qemu.example:             },
    qemu.example:             "hw_timestamp_filters": [],
    qemu.example:             "ipv4": {
    qemu.example:                 "address": "127.0.0.1",
    qemu.example:                 "broadcast": "",
    qemu.example:                 "netmask": "255.0.0.0",
    qemu.example:                 "network": "127.0.0.0"
    qemu.example:             },
    qemu.example:             "ipv6": [
    qemu.example:                 {
    qemu.example:                     "address": "::1",
    qemu.example:                     "prefix": "128",
    qemu.example:                     "scope": "host"
    qemu.example:                 }
    qemu.example:             ],
    qemu.example:             "mtu": 65536,
    qemu.example:             "promisc": false,
    qemu.example:             "timestamping": [],
    qemu.example:             "type": "loopback"
    qemu.example:         },
    qemu.example:         "lsb": {},
    qemu.example:         "lvm": {
    qemu.example:             "lvs": {
    qemu.example:                 "root": {
    qemu.example:                     "size_g": "3.39",
    qemu.example:                     "vg": "rl_template"
    qemu.example:                 },
    qemu.example:                 "swap": {
    qemu.example:                     "size_g": "0.49",
    qemu.example:                     "vg": "rl_template"
    qemu.example:                 }
    qemu.example:             },
    qemu.example:             "pvs": {
    qemu.example:                 "/dev/vda2": {
    qemu.example:                     "free_g": "0",
    qemu.example:                     "size_g": "3.88",
    qemu.example:                     "vg": "rl_template"
    qemu.example:                 }
    qemu.example:             },
    qemu.example:             "vgs": {
    qemu.example:                 "rl_template": {
    qemu.example:                     "free_g": "0",
    qemu.example:                     "num_lvs": "2",
    qemu.example:                     "num_pvs": "1",
    qemu.example:                     "size_g": "3.88"
    qemu.example:                 }
    qemu.example:             }
    qemu.example:         },
    qemu.example:         "machine": "x86_64",
    qemu.example:         "machine_id": "692a80dbcf304dcb81e40c0683b17ebf",
    qemu.example:         "memfree_mb": 2450,
    qemu.example:         "memory_mb": {
    qemu.example:             "nocache": {
    qemu.example:                 "free": 2656,
    qemu.example:                 "used": 191
    qemu.example:             },
    qemu.example:             "real": {
    qemu.example:                 "free": 2450,
    qemu.example:                 "total": 2847,
    qemu.example:                 "used": 397
    qemu.example:             },
    qemu.example:             "swap": {
    qemu.example:                 "cached": 0,
    qemu.example:                 "free": 499,
    qemu.example:                 "total": 499,
    qemu.example:                 "used": 0
    qemu.example:             }
    qemu.example:         },
    qemu.example:         "memtotal_mb": 2847,
    qemu.example:         "module_setup": true,
    qemu.example:         "mounts": [
    qemu.example:             {
    qemu.example:                 "block_available": 485878,
    qemu.example:                 "block_size": 4096,
    qemu.example:                 "block_total": 886272,
    qemu.example:                 "block_used": 400394,
    qemu.example:                 "device": "/dev/mapper/rl_template-root",
    qemu.example:                 "fstype": "xfs",
    qemu.example:                 "inode_available": 1746239,
    qemu.example:                 "inode_total": 1777664,
    qemu.example:                 "inode_used": 31425,
    qemu.example:                 "mount": "/",
    qemu.example:                 "options": "rw,seclabel,relatime,attr2,inode64,logbufs=8,logbsize=32k,noquota",
    qemu.example:                 "size_available": 1990156288,
    qemu.example:                 "size_total": 3630170112,
    qemu.example:                 "uuid": "047e9572-16be-4de2-a90d-907461abdc89"
    qemu.example:             },
    qemu.example:             {
    qemu.example:                 "block_available": 213560,
    qemu.example:                 "block_size": 4096,
    qemu.example:                 "block_total": 259584,
    qemu.example:                 "block_used": 46024,
    qemu.example:                 "device": "/dev/vda1",
    qemu.example:                 "fstype": "xfs",
    qemu.example:                 "inode_available": 523979,
    qemu.example:                 "inode_total": 524288,
    qemu.example:                 "inode_used": 309,
    qemu.example:                 "mount": "/boot",
    qemu.example:                 "options": "rw,seclabel,relatime,attr2,inode64,logbufs=8,logbsize=32k,noquota",
    qemu.example:                 "size_available": 874741760,
    qemu.example:                 "size_total": 1063256064,
    qemu.example:                 "uuid": "fc3e82af-aa80-4325-92c8-05ae2724ddd7"
    qemu.example:             }
    qemu.example:         ],
    qemu.example:         "nodename": "template",
    qemu.example:         "os_family": "RedHat",
    qemu.example:         "pkg_mgr": "dnf",
    qemu.example:         "proc_cmdline": {
    qemu.example:             "BOOT_IMAGE": "(hd0,msdos1)/vmlinuz-4.18.0-305.3.1.el8_4.x86_64",
    qemu.example:             "crashkernel": "auto",
    qemu.example:             "rd.lvm.lv": [
    qemu.example:                 "rl_template/root",
    qemu.example:                 "rl_template/swap"
    qemu.example:             ],
    qemu.example:             "resume": "/dev/mapper/rl_template-swap",
    qemu.example:             "ro": true,
    qemu.example:             "root": "/dev/mapper/rl_template-root"
    qemu.example:         },
    qemu.example:         "processor": [
    qemu.example:             "0",
    qemu.example:             "GenuineIntel",
    qemu.example:             "QEMU Virtual CPU version 2.5+"
    qemu.example:         ],
    qemu.example:         "processor_cores": 1,
    qemu.example:         "processor_count": 1,
    qemu.example:         "processor_threads_per_core": 1,
    qemu.example:         "processor_vcpus": 1,
    qemu.example:         "product_name": "KVM",
    qemu.example:         "product_serial": "NA",
    qemu.example:         "product_uuid": "NA",
    qemu.example:         "product_version": "RHEL 7.6.0 PC (i440FX + PIIX, 1996)",
    qemu.example:         "python": {
    qemu.example:             "executable": "/usr/libexec/platform-python",
    qemu.example:             "has_sslcontext": true,
    qemu.example:             "type": "cpython",
    qemu.example:             "version": {
    qemu.example:                 "major": 3,
    qemu.example:                 "micro": 8,
    qemu.example:                 "minor": 6,
    qemu.example:                 "releaselevel": "final",
    qemu.example:                 "serial": 0
    qemu.example:             },
    qemu.example:             "version_info": [
    qemu.example:                 3,
    qemu.example:                 6,
    qemu.example:                 8,
    qemu.example:                 "final",
    qemu.example:                 0
    qemu.example:             ]
    qemu.example:         },
    qemu.example:         "python_version": "3.6.8",
    qemu.example:         "real_group_id": 0,
    qemu.example:         "real_user_id": 0,
    qemu.example:         "selinux": {
    qemu.example:             "config_mode": "enforcing",
    qemu.example:             "mode": "enforcing",
    qemu.example:             "policyvers": 33,
    qemu.example:             "status": "enabled",
    qemu.example:             "type": "targeted"
    qemu.example:         },
    qemu.example:         "selinux_python_present": true,
    qemu.example:         "service_mgr": "systemd",
    qemu.example:         "ssh_host_key_ecdsa_public": "AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBCDTW9IEsJSAW0luoa+G13VoFfdXG6g+B13VEKFCIcsyJryhniQETmBkNGeSUCxBhIVyYW0sGyYgMFIdh7WsF1o=",
    qemu.example:         "ssh_host_key_ed25519_public": "AAAAC3NzaC1lZDI1NTE5AAAAIDCIr8LhuvPAm+nY/dDIuxg5TsvfHZt6M2gvw3Q4Xita",
    qemu.example:         "ssh_host_key_rsa_public": "AAAAB3NzaC1yc2EAAAADAQABAAABgQDmJn32qIikG4M41oHbnaXIx3FbKm0fJJwnzZJm0unwvn4gIimadCT+scG8hbNR3Mpm0C9bnlsl3mc6Dh77tKE1Un8fpGOhiM8tm/gofXyn/+AbsRBpspq2rOorUCyUYgSdLZlIXdxsZeKaj72IjPh4PmSAV7zLsIPUliOkGl7HX6Sm2VhN5upTjeEFxsrkI2P996doJ8RIQpMJgkbVoy7c0j/drIz3emVW0TM7eVhpg8YOJs6X3+k0sS6VTCTVP1fW2HhVwD5+JXviESofbNAPf2OqzYG34FLmX7C6J988+Zz9SZfLG2FgQNCZZlqOKw8zwG/C8bjX/H2Qw1X0PtPlhUvdeTuJ2XPqdMr+c9CQfYYc3FzaEkOteT94iJdCqqazW/YIGFExWFWbZ0nhee1KJElSRjfI+1zZbdu83/gsCjljig49ydGShIPhPegFVNn/ZXxgXwbB0UnYayPiLRL/PhBKkcldUMIyoQ06n3OSIwikq/EOaTw2qVjeXAbdS8E=",
    qemu.example:         "swapfree_mb": 499,
    qemu.example:         "swaptotal_mb": 499,
    qemu.example:         "system": "Linux",
    qemu.example:         "system_capabilities": [
    qemu.example:             "cap_chown",
    qemu.example:             "cap_dac_override",
    qemu.example:             "cap_dac_read_search",
    qemu.example:             "cap_fowner",
    qemu.example:             "cap_fsetid",
    qemu.example:             "cap_kill",
    qemu.example:             "cap_setgid",
    qemu.example:             "cap_setuid",
    qemu.example:             "cap_setpcap",
    qemu.example:             "cap_linux_immutable",
    qemu.example:             "cap_net_bind_service",
    qemu.example:             "cap_net_broadcast",
    qemu.example:             "cap_net_admin",
    qemu.example:             "cap_net_raw",
    qemu.example:             "cap_ipc_lock",
    qemu.example:             "cap_ipc_owner",
    qemu.example:             "cap_sys_module",
    qemu.example:             "cap_sys_rawio",
    qemu.example:             "cap_sys_chroot",
    qemu.example:             "cap_sys_ptrace",
    qemu.example:             "cap_sys_pacct",
    qemu.example:             "cap_sys_admin",
    qemu.example:             "cap_sys_boot",
    qemu.example:             "cap_sys_nice",
    qemu.example:             "cap_sys_resource",
    qemu.example:             "cap_sys_time",
    qemu.example:             "cap_sys_tty_config",
    qemu.example:             "cap_mknod",
    qemu.example:             "cap_lease",
    qemu.example:             "cap_audit_write",
    qemu.example:             "cap_audit_control",
    qemu.example:             "cap_setfcap",
    qemu.example:             "cap_mac_override",
    qemu.example:             "cap_mac_admin",
    qemu.example:             "cap_syslog",
    qemu.example:             "cap_wake_alarm",
    qemu.example:             "cap_block_suspend",
    qemu.example:             "cap_audit_read",
    qemu.example:             "38",
    qemu.example:             "39+ep"
    qemu.example:         ],
    qemu.example:         "system_capabilities_enforced": "True",
    qemu.example:         "system_vendor": "Red Hat",
    qemu.example:         "uptime_seconds": 61,
    qemu.example:         "user_dir": "/root",
    qemu.example:         "user_gecos": "root",
    qemu.example:         "user_gid": 0,
    qemu.example:         "user_id": "root",
    qemu.example:         "user_shell": "/bin/bash",
    qemu.example:         "user_uid": 0,
    qemu.example:         "userspace_architecture": "x86_64",
    qemu.example:         "userspace_bits": "64",
    qemu.example:         "virtualization_role": "guest",
    qemu.example:         "virtualization_type": "kvm"
    qemu.example:     }
    qemu.example: }
```
