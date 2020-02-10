Openssl Generate Self-signed Certificate for https Demo
=======================================================

注意：下面的写法是旧的，生成的证书已经不被chrome承认：

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

下面的写法是新的，主要是用到了SAN：

```
openssl req -x509 -newkey rsa:4096 -sha256 -days 3650 -nodes \
  -keyout example.key -out example.crt -extensions san -config \
  <(echo "[req]"; 
    echo distinguished_name=req; 
    echo "[san]"; 
    echo subjectAltName=DNS:example.com,DNS:example.net,IP:10.0.0.1
    ) \
  -subj /CN=example.com
```

- `-config`：这块是因为对于大多数openssl版本，`san`相关参数只能通过config file的样式传入
