# Client SSL Authentication with Docker Containers

## Requirements
- Docker
- docker-compose

## Installation

Launch the containers
```bash
docker-compose up
```

## Links

- [Proxy](https://localhost:9443/)
- [NGINX](https://localhost/)


### How to create the certificates :

```bash
cd certifs-appli

# Create the CA certificate
openssl genrsa -out ca.key 4096
openssl req -new -x509 -days 365 -key ca.key -out ca.crt

# Create the Proxy Certificate request
openssl genrsa -out proxy.key 1024
openssl req -new -key proxy.key -out proxy.csr

# Create the NGINX Certificate request
openssl genrsa -out nginx.key 1024
openssl req -new -key nginx.key -out nginx.csr

# Sign your certificate requests with the CA
openssl x509 -req -days 365 -in proxy.csr -CA ca.crt -CAkey ca.key -set_serial 01 -out proxy.crt
openssl x509 -req -days 365 -in nginx.csr -CA ca.crt -CAkey ca.key -set_serial 01 -out nginx.crt
```
