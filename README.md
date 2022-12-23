# PHPOnDocker_with_PDO_OCI

This repo have a Dockerfile to create a cotainer with PHP with PDO_OCI and OCI8
<br>
<br>
This will generate a self-signed certificate for you to simulate an SSL connection on localhot (optional): 

```bash
openssl req -x509 -sha256 -newkey rsa:2048 -keyout certificate.key -out certificate.crt -days 1024 -nodes
```
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
To create the image

```bash
sudo docker compose --build
```

<br>
If you want to build the images:
<br>
To create the image

```bash
sudo docker compose up --build
```

## Screenshots:
PHP version:
<img src="https://raw.githubusercontent.com/hudsonventura/images/main/imagem_2022-12-23_141052919.png" alt="Alt text" title="Optional title">
<br>
<br>
Evidence OCI:
<img src="https://raw.githubusercontent.com/hudsonventura/images/main/imagem_2022-12-23_141032558.png" alt="Alt text" title="Optional title">