# CloudTP1 Hugo LORANT

## Prérequis
 - Le fichier Rocky-8.4-x86_64-minimal.iso doit etre present dans le dossier CloudTP1
 - Ansible doit être installé

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
