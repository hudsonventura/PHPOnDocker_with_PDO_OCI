# PHPOnDocker_with_PDO_OCI

This repo have a Dockerfile to create a cotainer with PHP with PDO_OCI and OCI8
<br>


This will generate a self-signed certificate for you to simulate an SSL connection on localhot (optional): 

```bash
openssl req -x509 -sha256 -newkey rsa:2048 -keyout certificate.key -out certificate.crt -days 1024 -nodes
```
<br>

To create the image

```bash
sudo docker compose --build
```

<br>

To up operate the container

```bash
sudo docker compose up 
sudo docker compose down
```