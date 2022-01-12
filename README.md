# Example: CA Certificates

This repo will show you how to have a static web server using self signed-certificates.

This repo uses Vagrant to create a virtual machine

Vagrant virtual machine
- ubuntu virtual machine starts
- Nginx webserver will be installed, configured and started
- TLS certificates will be generated and stored under ```/vagrant/ssl```

After this you will manually login to the Vagrant virtual machine and check the website and certificates being used on the server. 

More details on certificates [See the following documentation](https://jamielinux.com/docs/openssl-certificate-authority/index-full.html)

# Prerequisites

## Vagrant
Vagrant [See documentation](https://www.vagrantup.com/docs/installation)  
Virtualbox [See documentation](https://www.virtualbox.org/wiki/Downloads)


# How to

- Clone the repository to your local machine
```
git clone https://github.com/munnep/CA_certificate_authority.git
```
- Go to the directory
```
cd CA_certificate_authority
```
- start the Vagrant virtual machines
```
vagrant up
```
- login to the virtual machine **tf**
```
vagrant ssh
```
- Download the index.html to check if this succeeds
```
wget https://192.168.56.50.nip.io/index.html
```
- Check the TLS certificate being used
```
echo | openssl s_client -showcerts -servername 192.168.56.50.nip.io -connect 192.168.56.50.nip.io:443 2>/dev/null | openssl x509 -inform pem -noout -text
```
output:
```
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = CN, ST = GD, L = SZ, O = "Acme, Inc.", CN = Acme Root CA
        Validity
            Not Before: Jan 12 09:17:19 2022 GMT
            Not After : Jan 12 09:17:19 2023 GMT
        Subject: C = CN, ST = GD, L = SZ, O = "Acme, Inc.", CN = 192.168.56.50.nip.io

```
- exit out of the vagrant machine
```
exit
```
- try the same wget command from your local machine
```
wget https://192.168.56.50.nip.io/index.html              
```
output:      
```
--2022-01-12 10:21:43--  https://192.168.56.50.nip.io/index.html
Resolving 192.168.56.50.nip.io (192.168.56.50.nip.io)... 192.168.56.50
Connecting to 192.168.56.50.nip.io (192.168.56.50.nip.io)|192.168.56.50|:443... connected.
ERROR: cannot verify 192.168.56.50.nip.io's certificate, issued by ‘CN=Acme Root CA,O=Acme\\, Inc.,L=SZ,ST=GD,C=CN’:
  Unable to locally verify the issuer's authority.
To connect to 192.168.56.50.nip.io insecurely, use `--no-check-certificate'.
```
You get this error because the CA created within the Virtual Machine isn't trusted by your local machine. 
- destroy the vagrant machine
```
vagrant destroy
```














