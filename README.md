# ignition_math_docker

Docker with the Ignition math library installed and configured.

- [Tested Environment](#Tested-environment)
- [Installation](#Installation)
- [Usage](#Usage)

# Tested Environment

- Ubuntu 16.04
- Ubuntu 18.04

# Installation

- Install docker on your computer:

```
sudo apt-get install curl
curl -fsSL https://get.docker.com -o get-docker.sh
sh get-docker.sh
```

- Run these configurations to remove the need of running docker as a root user:

```
sudo groupadd docker
sudo usermod -aG docker "usuario" (Trocar "usuario" pelo nome do seu usuário. Ex: sudo usermod -aG docker ximenes)
```

- Restart you computer to make the changes above valid.

- Install `docker-compose` on your computer:

```
sudo apt-get install -y python3-pip
sudo python3 -m pip install docker-compose
```

- Clone this repository:

```
sudo apt-get install -y git
git clone https://github.com/ximenesfel/ignition_math_docker.git
cd ignition_math_docker
```

- Run docker container using `docker-compose`:

```
docker-compose up -d
```

- Check if the container is up:

```
docker-compose ps
```

Resposta do comando se tiver rodando corretamente.

```
                Name                    Command    State   Ports
----------------------------------------------------------------
ignition_math_docker_ignition_math_1   /bin/bash   Up           
```


# Usage

- Go into the bash terminal of the ignition_math container:

```
docker-compose exec ignition_math bash

root@14f2b2451330:~# 
```

Now you're inside the container with the ign_math project installed. To check run the `ls` command and you should be this on the terminal:

```
ign_math
```
