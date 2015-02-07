Common Ansible Role for Ubuntu Server:
---
 With this role you can prepare your machine to do the following tasks:
  
 - Install the minimum essential packages
     - build-essential
     - python-software-properties
     - git
 - Setting Hostname 
 - Add the additional sudo user with passwordless sudo option
 - Enable the Multiverse repository
 - OpenNTPD Installation
 - Timezone Configuration
 - VIM-nox Installation
 - SSMTP Installation and Configuration with GMail for Sending System Alerts
 - Automatic Security Updates Installation
 - Disable the Default UFW
 - Fail2Ban Installation and Configuration

### To use this Role:

 Edit the `site.yml` file, mentioned this role:

```yaml
---
 - hosts: server
   sudo: True
   gather_facts: True
   roles:
     - common
```

After that edit the encrypted `vars/main.yml` file with this command:
```
ansible-vault edit vars/main.yml
```
**Note:** Default vault password is `tendo`

> Change these values as per your requirement.

```yaml
---
 # Username & Password that we want to create on the Linux Server
 username: arbab
 password: $6$ZdqWXxLVpGlD$T86H51YzBeFlTIDWIRMfkhzuB6KxzXXtJ8jAbBXvlVCj.biPoN8rgz3iFgXU9OZr7DAmveHnvViAyx6F/FfZ81
 # Mentioned your GMAIL ID and Password Here
 gmail_id: ansible@gmail.com
 gmail_password: tendo123
 # Fail2Ban will send the Alerts on this Email
 receiver_mail: tendo.linux@gmail.com
 # Hostname Settings
 default_ip: 127.0.1.1 #ip address of the server either public or private
 hostname: tendo       #hostname of the Linux Server
 domain: geek.com      #Domain name that will be used in fqdn
 fqdn: "{{ hostname }}.{{ domain }}" #FQDN that will be used in hosts file
 # Timezone Setting
 timezone: "Asia/Karachi"
```
**Note** that the password for the user are also hashed. To generate the crypted passwords for the user module, use the following command(s):
```shell
# The whois package makes the mkpasswd command available on Ubuntu
$ sudo apt-get install -y whois

# Create a password hash
$ mkpasswd --method=SHA-512
Password:
This will generate a hashed password for you to use with the user module.
```