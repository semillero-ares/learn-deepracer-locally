# Solución de errores

## Permiso denegado en Docker

Cuando aparece el error:

```txt
dial unix /var/run/docker.sock: connect: permission denied
```

Deberemos instalar `acl` y modificar los permisos de Docker con los siguientes comandos.

```sh
sudo apt install acl
sudo setfacl --modify user:$USER:rw /var/run/docker.sock
```

## Verificar que el docker esta corriendo

```sh
docker ps -a 
```

## Docker no running

https://askubuntu.com/questions/1437128/docker-service-wont-start-on-ubuntu-22-04-on-wsl2

Si el docker no abre ... 

1. sudo update-alternatives --config iptables
2. Type number "1" and press Enter to select "iptables-legacy"
3. sudo service docker start


## Para el error (1)

region: 'us-east-1'