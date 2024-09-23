### Step 1 - Install and Config easy-rsa on Ubuntu
At some point, usually multiple points, a sysadmin/operator/devops/whatever needs a certificate authority (CA). At first this seems easy, then it seems hard, then you think you know what 
you are doing but you don’t, and I’m not sure you ever do. But you still need that CA. Even if you are using some sort of fancy certificate managment system (such as Hashicorp Vault) you 
still probably need to manage your top level CA.


1-1- install easy-rsa
```yml
sudo apt install easy-rsa
dpkg --list easy-rsa

Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name           Version        Architecture Description
+++-==============-==============-============-=================================
ii  easy-rsa       3.0.8-1ubuntu1 all          Simple shell based CA utility

```
1-2- Config CA Server
```yml
cd /usr/share/easy-rsa
# RUN Commands for easy-rsa on this path
./easyrsa init-pki

# show some like this 
init-pki complete; you may now create a CA or requests.
Your newly created PKI dir is: /usr/share/easy-rsa/pki


