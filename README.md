# home_network_ansible

;rtx1210            IN A        172.16.1.1
;l3-3560            IN A        172.28.1.2
;l2-2960            IN A        172.28.1.3

$ vi /etc/ansible/ansible.cfg
[defaults]
host_key_checking = False

```shell
sudo apt install python3-pip
pip3 install paramiko
ansible-galaxy collection install cisco.ios
ansible-playbook -i hosts/all.yml -l l3 --ask-vault-pass all.yml
```
