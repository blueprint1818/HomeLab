The Easiest way to make an authentik server is the following

- make a directory in your docker server "mkdir authentik"
- cd into the authentik directory
- do "wget https://goauthentik.io/docker-compose.yml"
- if you dont have a password generator then do "sudo apt-get install -y pwgen"
- then do the following command to generate a secret key into the config file of your docker-compose
echo "PG_PASS=$(pwgen -s 40 1)" >> .env
echo "AUTHENTIK_SECRET_KEY=$(pwgen -s 50 1)" >> .env
- to enable error reporting do "echo "AUTHENTIK_ERROR_REPORTING__ENABLED=true" >> .env"
- By default, authentik listens internally on port 9000 for HTTP and 9443 for HTTPS. To change the exposed ports to 80 and 443, you can set the following variables in .env
COMPOSE_PORT_HTTP=80
COMPOSE_PORT_HTTPS=443
- after that all you need to do is run the docker compose file. Do the following commands
docker-compose pull
docker-compose up -d
- once the compose has started and is running good go onto the web gui for it and type this at the end to make it work properly https://ipofauthentik:9443/initialsetup