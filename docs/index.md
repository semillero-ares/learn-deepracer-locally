# Aprendiendo a usar DeepRacer localmente


https://deepracer.com

https://student.deepracer.com


https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

Add Docker's official GPG key:

```sh
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

Add the repository to Apt sources:
```sh
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

https://aws-deepracer-community.github.io/deepracer-for-cloud/windows.html

```sh
sudo apt-get install jq awscli python3-boto3 docker-compose 
```

https://stackoverflow.com/questions/44678725/cannot-connect-to-the-docker-daemon-at-unix-var-run-docker-sock-is-the-docker

```sh
sudo systemctl start docker
sudo docker run hello-world
```

https://aws-deepracer-community.github.io/deepracer-for-cloud/installation.html

```sh
git clone https://github.com/aws-deepracer-community/deepracer-for-cloud.git
```

```
aws configure --profile minio
```

## Solucionando el error

Error : `dial unix /var/run/docker.sock: connect: permission denied`

```sh
sudo apt install acl
sudo setfacl --modify user:jammy:rw /var/run/docker.sock
source bin/activate.sh 
```

## Lista de comandos
https://aws-deepracer-community.github.io/deepracer-for-cloud/reference.html

```sh
dr-upload-custom-files
dr-stop-training
dr-start-training
dr-stop-viewer
dr-start-viewer
```

## Verificar que el docker esta corriendo

```sh
docker ps -a 
```
### Para hacer el streaming en YouTube del entrenamiento

https://youtu.be/YVmlPvEioMA?feature=shared

Se necesita tener instalado OBS. 
