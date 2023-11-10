# Usando el DeepRacer en local

Empecemos explicando que es el DeepRacer:

DeepRacer es una plataforma de aprendizaje, competencia y diversión creada por Amazon AWS, que nos permite aprender sobre _machine learning_ y ademas competir a nivel mundial con diferentes desarrolladores. 

Existen dos versiones para participar en competencias:

- [La versión abierta](https://deepracer.com) que tiene 10 horas de entrenamiento gratuitas los primeros 30 días.
- [La versión estudiante](https://student.deepracer.com) que tiene 10 horas de entrenamiento gratuitas cada mes. 

Una mejor forma de entrenar tu modelo y probarlo es entrenarlo en tu computador y usar esas 10 horas para enviar tus modelos a competir. 

Para instalar DeepRacer en tu computador necesitaremos tener [ubuntu](https://aws-deepracer-community.github.io/deepracer-for-cloud/installation.html) o [WSL](https://aws-deepracer-community.github.io/deepracer-for-cloud/windows.html) (ubuntu sobre windows). También esta la opción de instalarlo [directamente en windows](https://github.com/PhoenixDai/deepracer-windows) pero no lo recomiendo. 

## Instalación en WSL o Ubuntu

DeepRacer en local hace uso de **Docker** que es un gestor de contenedores que permiten instalar y correr facilmente todo lo necesario para entrenar y probar nuestro modelos en el computador. 

### Instalación de Docker

Para instalar docker en nuestro computador, lo haremos usando el repositorio oficial ([instructivo detallado](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)). Y seguiremos los pasos resumidos a continuación.

- Instalaremos una clave de seguridad para poder instalar docker:

```sh
sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

- Agregamos el repositorio a las fuentes apt:

```sh
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

Los pasos anteriores solo deben hacerse una vez.

- Instalamos las dependencias ([1])

[1]:https://aws-deepracer-community.github.io/deepracer-for-cloud/windows.html "Instalación de DeepRacer en Windows"

```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin jq awscli python3-boto3 docker-compose -y
```

- Verificar que Docker esta funcionando

```sh
sudo service docker status
```

En caso de no estar funcionando inicializar el servicio como se muestra a continuación ([2]):

[2]: https://stackoverflow.com/questions/44678725/cannot-connect-to-the-docker-daemon-at-unix-var-run-docker-sock-is-the-docker "Solucionando el servicio de docker"

```sh
sudo systemctl start docker 
sudo docker run hello-world
```

## Instalación de DeepRacer

Para la instalación ([3]) de DeepRacer debemos clonar el repositorio `git`:

[3]: <https://aws-deepracer-community.github.io/deepracer-for-cloud/installation.html> "Instalación general de DeepRacer"

```sh
git clone https://github.com/aws-deepracer-community/deepracer-for-cloud.git
```

una vez clonado vamos a la carpeta de `deepracer-for-cloud`

```sh
cd deepracer-for-cloud
```

y seguiremos los siguientes pasos: 

- Configuraremos el servidor que guardará los datos de entrenamiento:

```sh
aws configure --profile minio
```

Aquí es importante tener en cuenta las siguientes recomendaciones:

- El _"AWS Secret Access Key"_ debe ser mayor de 4 carácteres
- La _"Default region name"_ debe ser `us-east-1`.

Luego de esta configuración debemos inicializar todos los procesos para el DeepRacer con el siguiente comando

```sh
./bin/init.sh
```

Aquí ya tenemos instalado y configurado nuestra DeepRacer en local

## Usando el DeepRacer en Local

Vamos a tener dos terminales abiertas ubicadas en la carpeta `deepracer-for-cloud` y haremos los siguiente en cada terminal:

### En la Terminal 1:

```sh
source bin/activate.sh
dr-stop-viewer
dr-start-viewer
```

### En la Terminal 2:

```sh
source bin/activate.sh
dr-update-env
dr-update
dr-upload-custom-files
dr-stop-evaluation
dr-stop-training
dr-start-training -w
```

Todos estos comandos pueden ser consultados [en la página de referencia](https://aws-deepracer-community.github.io/deepracer-for-cloud/reference.html)

## Modificando la función recompensa

Para modificar la función recompensa debemos modificar el archivo `/deepracer-for-cloud/custom_files/reward_function.py` y correr los comandos anteriores en los dos terminales.