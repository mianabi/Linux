## SSH Key Auth With eval
### 1. ensure that ssh Service is Running
```yml
systemctl status ssh
systemctl start ssh
```
### 2. in vm1: Generate Key in VM1
```yml
ssh-keygen -t rsa (Enter passphrase)
ls -ltrha /home/majidm/
cd .ssh/
ls
```
### 3. in vm2(Target): Generate Key in VM2
```yml
ssh-keygen -t rsa
ls -ltrha /home/majid/
cd .ssh/
ls
```
### 4. in vm1: Copy key to VM2
```yml
ssh-copy-id majid@192.168.61.131
ssh majid@192.168.61.131
#then enter passphrase
eval $(ssh-agent)
ssh-add
ssh majid@192.168.61.131
```
then Enter in VM2 Without passphrase
