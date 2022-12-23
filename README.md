# PHPOnDocker_with_PDO_OCI

This repo have a Dockerfile to create a cotainer with PHP with PDO_OCI and OCI8
<br>


<br>

If you want just up contaners with PHP FPM with OCI and PDO_OCI and Nginx just do:

```bash
sudo docker compose up
```
<br>
and this to down the containers

```bash
sudo docker compose down
```

<br>
If you want to build the images:

```bash
sudo docker compose up --build
```

<br>
<br>

### Optional zone
<br>
This will generate a self-signed certificate for you to simulate an SSL connection on localhot (optional): 

```bash
cd configs/cert/
openssl req -x509 -sha256 -newkey rsa:2048 -keyout certificate.key -out certificate.crt -days 1024 -nodes
```
And uncomment the below lines on file configs/app.vhost

```
#listen 443 ssl;
#ssl_certificate     /etc/nginx/cert/certificate.crt;
#ssl_certificate_key /etc/nginx/cert/certificate.key;
```
At this moment you will receive a error on certificate, but the SSL is able.
If you want to add a valid certificate, just replace the key a crt file at configs/cert

## Screenshots:
<img src="https://raw.githubusercontent.com/hudsonventura/images/main/imagem_2022-12-23_141052919.png" alt="Alt text" title="Optional title">
<br>
<br>
<img src="https://raw.githubusercontent.com/hudsonventura/images/main/imagem_2022-12-23_141032558.png" alt="Alt text" title="Optional title">