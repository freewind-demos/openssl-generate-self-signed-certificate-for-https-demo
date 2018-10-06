Openssl Generate Self-signed Certificate for https Demo
=======================================================

```
$ openssl req -x509 -newkey rsa:4096 -keyout key.pem -out cert.pem -nodes -subj '/CN=localhost' -days 365
```

- `-nodes`: No DES, 不需要设置密码以及相关信息


```
Generating a 4096 bit RSA private key
...................................................................................................++
......................................++
writing new private key to 'key.pem'
-----
```

之后，将会多出一个`cert.pem`和`key.pem`文件。