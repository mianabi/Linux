1.
```yml
vim /etc/netplan/01-network-manager-all.yaml
```
2.
```yml
netplan try
apt install bind9 bind9-utils
cd /etc/bind/
vim named.conf.local
```
3.
```yml
vim named.conf.options
```
4.
```yml
etc/bind/zones# vim sana.com.deb
```
5.
```yml
/etc/bind/reverse# vim 1.168.192.in-addr.arpa
```
6. Test DNS Server
```yml

named-checkconf
rndc reload
systemctl reload bind9

nslookup 
  > server 127.0.0.1 …
  > sana.com …
  >set q=ns
  > sana.com …
  >set q=a
  >ns1.sana.com …
```

### Configs in slave DNS:
```yml
vim /etc/netplan/01-network-manager-all.yaml
```

