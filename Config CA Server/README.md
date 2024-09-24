in Complete and Real Senario, First install and Config Ca Server in Linux(ubuntu) by easy-rsa and then in Step 2 As an enterprise client, we generate a request file (CSR) by the received public key and present it to the official of the CA server, and in the third step, we generate a certificate in the CA server and deliver it to the client.

### Step 1 - Install and Config easy-rsa on Ubuntu
At some point, usually multiple points, a sysadmin/operator/devops/whatever needs a certificate authority (CA). At first this seems easy, then it seems hard, then you think you know what 
you are doing but you don’t, and I’m not sure you ever do. But you still need that CA. Even if you are using some sort of fancy certificate managment system (such as Hashicorp Vault) you 
still probably need to manage your top level CA in your Organization.


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

# to create private and public key on CA Server run below Command
 ./easyrsa build-ca

# and enter Passphrase and General Common Name For CA Server. Some Like this:
nter New CA Key Passphrase: 
Re-Enter New CA Key Passphrase: 
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Common Name (eg: your user, host, or server name) [Easy-RSA CA]: *MyCA*

CA creation complete and you may now import and sign cert requests.
Your new CA certificate file for publishing is at:
/usr/share/easy-rsa/pki/ca.crt
```
public key of CA Server Generate in path /usr/share/easy-rsa/ca.crt and And this public key should be given to customers or clients to trust. Now, any computer or server that has this file will be trusted by the Linux server.

in path /usr/share/easy-rsa/private There is a ca.crt file that is very important and must be protected.

Note: You can Trust public key in linux Server(client):

* Copy ca.crt file to path /etc/pki/ca-trust/source/anchors and run this command:
```yml
update-ca-trust
```

### Step 2 - Generate CSR file Like a customer(in linux)
in this sample we want to create CSR file to my site(www.test.com)
2-1- Create private key for ourselves(Client)
```yml
openssl genrsa -aes256 -out test.com.key 2048
# entar Passphrase
```

2-2- now Create CSR file:
```yml
openssl req -new -key test.com.key -out test.com.csr
# enter Passphrase that entered in Step 2-1 and enter Country, City, organization and OU and enter Common name(cn) that is very important(*.test.com or www.test.com)
```
We give this CSR file(test.com.csr) to the official of the CA server to get the Certificate

### Step 3 - Generate Certificate

3-1- in Ca Server run this Command on path /usr/share/easy-rsa
```yml
cd /usr/share/easy-rsa
./easyrsa import-req test.com.csr SomeClient
# SomeClient is Optional Name For Client
./easyrsa sign-req server SomeClient
# Enter Pass of CA Server and enter to create SomeClient.crt
```

3-2- We must Deliver file SomeClient.crt in folder issued to Client.

3-2- for Revokation of Delivered Certificate enter this Command
```yml
./easyrsa revoke SomeClient.crt
```








