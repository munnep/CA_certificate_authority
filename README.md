# CA_certificate_authority



# Create the root pair
```
mkdir /root/ca
cd /root/ca
mkdir certs crl newcerts private
chmod 700 private
touch index.txt
echo 1000 > serial
```

Create the root key
```
openssl genrsa -aes256 -out private/ca.key.pem 4096

chmod 400 private/ca.key.pem
```

```
openssl req -config openssl.cnf \
      -key private/ca.key.pem \
      -new -x509 -days 7300 -sha256 -extensions v3_ca \
      -out certs/ca.cert.pem
```


```
chmod 444 certs/ca.cert.pem
```

verify it
```
openssl x509 -noout -text -in certs/ca.cert.pem
```

# create the intermediate pair

```
mkdir /root/ca/intermediate
```

```
cd /root/ca/intermediate
mkdir certs crl csr newcerts private
chmod 700 private
touch index.txt
echo 1000 > serial
```

## 
```
# cd /root/ca
# openssl genrsa -aes256 \
      -out intermediate/private/intermediate.key.pem 4096

Enter pass phrase for intermediate.key.pem: secretpassword
Verifying - Enter pass phrase for intermediate.key.pem: secretpassword

# chmod 400 intermediate/private/intermediate.key.pem
```