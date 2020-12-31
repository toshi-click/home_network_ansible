# home_network_ansible

;rtx1210            IN A        172.16.1.1
;l3-3560            IN A        172.28.1.2
;l2-2960            IN A        172.28.1.3



```shell
ansible-galaxy collection install cisco.ios
ansible-playbook -i hosts/all.yml -l l3 --ask-vault-pass all.yml
```
