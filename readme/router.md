
## ipv4フィルター
```shell
ip lan2 secure filter in 4010 4020 4021 4022 4221 4222 4699
ip lan2 secure filter out 4998 4999 dynamic 4080 4081 4082 4083 4084 4085 4098 4099
ip filter 4010 reject 0.0.0.0/8,10.0.0.0/8,127.0.0.0/8,169.254.0.0/16,172.16.0.0/12,192.168.0.0/16
ip filter 4020 pass * * icmp * *
ip filter 4021 pass * * established * *
ip filter 4022 pass * * tcp * ident
ip filter 4221 reject * * udp,tcp 135,137-139,445 *
ip filter 4222 reject * * udp,tcp * 135,137-139,445
ip filter 4699 reject * *
ip filter 4998 pass 172.16.0.1-172.16.254.254 *
ip filter 4999 pass 172.28.0.1-172.28.254.254 *
ip filter dynamic 4080 * * ftp
ip filter dynamic 4081 * * www
ip filter dynamic 4082 * * domain
ip filter dynamic 4083 * * smtp
ip filter dynamic 4084 * * pop3
ip filter dynamic 4085 * * submission
ip filter dynamic 4098 * * tcp
ip filter dynamic 4099 * * udp
```

## ipフィルター
解放したいアドレス・ポートがあれば6699以前に入れる
```shell
ipv6 prefix 1 ra-prefix@lan2::/64
ipv6 lan2 dhcp service client ir=on 
ipv6 lan2 secure filter in 6030 6031 6032 6110 6120 6699
ipv6 lan2 secure filter out 6999 dynamic 6080 6081 6082 6083 6084 6085 6098 6099
ipv6 filter 6030 pass * * icmp6 * *
ipv6 filter 6031 pass * * tcp * ident
ipv6 filter 6032 pass * * udp * 546
# Windowsのファイル共有をReject
ipv6 filter 6110 reject * * udp,tcp 135,137-139,445 *
ipv6 filter 6120 reject * * udp,tcp * 135,137-139,445
ipv6 filter 6699 reject * *
ipv6 filter 6999 pass * * * * *

ipv6 filter dynamic 6080 * * ftp
ipv6 filter dynamic 6081 * * domain
ipv6 filter dynamic 6082 * * www
ipv6 filter dynamic 6083 * * smtp
ipv6 filter dynamic 6084 * * pop3
ipv6 filter dynamic 6085 * * submission
ipv6 filter dynamic 6098 * * tcp
ipv6 filter dynamic 6099 * * udp
```

## dhcp server setting
```shell
dhcp service server
dhcp scope 1 172.16.0.2-172.16.254.254/16
dhcp scope bind 1 172.16.11.10 ethernet 98:41:5c:e3:1b:fc
dhcp scope bind 1 172.16.100.12 ethernet 34:de:1a:59:1f:32
dhcp scope bind 1 172.16.77.21 ethernet b0:a4:60:c2:ce:05
dhcp scope bind 1 172.16.100.71 ethernet 00:25:22:a0:b0:4c
dhcp scope bind 1 172.16.100.106 ethernet 8c:25:05:db:3a:20
dhcp scope bind 1 172.16.100.107 ethernet 0c:9d:92:71:0c:bd
dhcp scope bind 1 172.16.100.108 ethernet dc:72:9b:c7:23:9f
dhcp scope bind 1 172.16.100.109 ethernet 1c:fe:2b:10:0d:8f
dhcp scope bind 1 172.16.100.205 ethernet 58:cb:52:7d:dc:a2
dhcp scope bind 1 172.16.100.210 ethernet 00:0b:82:91:bf:db
dhcp scope bind 1 172.16.100.211 ethernet f4:a9:97:48:c2:a2
dhcp scope bind 1 172.16.100.241 ethernet 24:5e:be:1f:34:c8
```

ip lan2 intrusion detection in on
ip lan2 intrusion detection in ip on reject=on
ip lan2 intrusion detection in ip-option on reject=on
ip lan2 intrusion detection in fragment on reject=on
ip lan2 intrusion detection in icmp on reject=on
ip lan2 intrusion detection in udp on reject=on
ip lan2 intrusion detection in tcp on reject=on
ip lan2 intrusion detection in default off
ip lan2 intrusion detection out on
ip lan2 intrusion detection out ftp on reject=on
ip lan2 intrusion detection out winny on reject=on
ip lan2 intrusion detection out share on reject=on
ip lan2 intrusion detection out default off
