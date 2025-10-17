# Ответ к ДЗ 4 «Оркестрация группой Docker контейнеров на примере Docker Compose»
## Задача 1
https://hub.docker.com/r/kokosananas/custom-nginx

## Задача 2
<img width="1591" height="424" alt="image" src="https://github.com/user-attachments/assets/1a11e358-3720-4bf4-81f5-2cf5774a1442" />

## Задача 3
<img width="1691" height="397" alt="image" src="https://github.com/user-attachments/assets/b4e1c13e-d221-4b3d-b452-80ebac30e144" />
docker attach присоединяет наш терминал к главному процессу (PID 1) контейнера. Нажатие Ctrl-C посылает этому процессу сигнал SIGINT. Главный процесс завершается и контейнер переходит в Exited

<img width="1199" height="161" alt="image" src="https://github.com/user-attachments/assets/0cca6d96-cc3b-4234-b0ef-c4b9a777edeb" />

<img width="996" height="426" alt="image" src="https://github.com/user-attachments/assets/3bfe74d0-49ae-4ea7-856c-3c17923e8f99" />

## Задача 4

<img width="945" height="519" alt="image" src="https://github.com/user-attachments/assets/1263211f-4e00-442e-8184-a2d575a012cb" />
<img width="1094" height="610" alt="image" src="https://github.com/user-attachments/assets/6ebe956b-d283-448b-88aa-151e199ad73a" />

## Задача 5

Last login: Fri Oct 17 06:03:30 2025 from 178.178.244.228
roman@devops-24-4:~$ mkdir -p ~/tmp/netology/docker/task5 && cd ~/tmp/netology/docker/task5
roman@devops-24-4:~/tmp/netology/docker/task5$ cat > compose.yaml <<'YAML'
version: "3"
services:
  portainer:
    network_mode: host
    image: portainer/portainer-ce:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
YAML
roman@devops-24-4:~/tmp/netology/docker/task5$ cat > docker-compose.yaml <<'YAML'
version: "3"
services:
  registry:
    image: registry:2
    ports:
      - "5000:5000"
YAML
roman@devops-24-4:~/tmp/netology/docker/task5$ docker compose up -d
WARN[0000] Found multiple config files with supported names: /home/roman/tmp/netology/docker/task5/compose.yaml, /home/roman/tmp/netology/docker/task5/docker-compose.yaml
WARN[0000] Using /home/roman/tmp/netology/docker/task5/compose.yaml
WARN[0000] /home/roman/tmp/netology/docker/task5/compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
[+] Running 9/9
 ✔ portainer Pulled                                                                               5.6s
   ✔ dd71b00e32eb Pull complete                                                                   0.5s
   ✔ 3ecc252cea9e Pull complete                                                                   0.6s
   ✔ c551c6af3241 Pull complete                                                                   1.2s
   ✔ 36afcd70bebe Pull complete                                                                   1.2s
   ✔ 4a8b81d70feb Pull complete                                                                   2.8s
   ✔ fc8377c924b2 Pull complete                                                                   3.1s
   ✔ c78e85a42631 Pull complete                                                                   3.1s
   ✔ 4f4fb700ef54 Pull complete                                                                   3.2s
[+] Running 1/1
 ✔ Container task5-portainer-1  Started                                                           1.6s
roman@devops-24-4:~/tmp/netology/docker/task5$ docker compose ps
WARN[0000] Found multiple config files with supported names: /home/roman/tmp/netology/docker/task5/compose.yaml, /home/roman/tmp/netology/docker/task5/docker-compose.yaml
WARN[0000] Using /home/roman/tmp/netology/docker/task5/compose.yaml
WARN[0000] /home/roman/tmp/netology/docker/task5/compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
NAME                IMAGE                           COMMAND        SERVICE     CREATED         STATUS         PORTS
task5-portainer-1   portainer/portainer-ce:latest   "/portainer"   portainer   2 minutes ago   Up 2 minutes
roman@devops-24-4:~/tmp/netology/docker/task5$ docker ps
CONTAINER ID   IMAGE                           COMMAND        CREATED         STATUS         PORTS     NAMES
744c3019a2b6   portainer/portainer-ce:latest   "/portainer"   2 minutes ago   Up 2 minutes             task5-portainer-1
roman@devops-24-4:~/tmp/netology/docker/task5$ cat > compose.yaml <<'YAML'
version: "3"
include:
  - docker-compose.yaml

services:
  portainer:
    network_mode: host
    image: portainer/portainer-ce:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
YAML
roman@devops-24-4:~/tmp/netology/docker/task5$ docker compose up -d
WARN[0000] Found multiple config files with supported names: /home/roman/tmp/netology/docker/task5/compose.yaml, /home/roman/tmp/netology/docker/task5/docker-compose.yaml
WARN[0000] Using /home/roman/tmp/netology/docker/task5/compose.yaml
WARN[0000] /home/roman/tmp/netology/docker/task5/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
WARN[0000] /home/roman/tmp/netology/docker/task5/compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
[+] Running 6/6
 ✔ registry Pulled                                                                               3.6s
   ✔ 44cf07d57ee4 Pull complete                                                                  1.0s
   ✔ bbbdd6c6894b Pull complete                                                                  1.1s
   ✔ 8e82f80af0de Pull complete                                                                  1.3s
   ✔ 3493bf46cdec Pull complete                                                                  1.3s
   ✔ 6d464ea18732 Pull complete                                                                  1.5s
[+] Running 3/3
 ✔ Network task5_default        Created                                                          0.0s
 ✔ Container task5-registry-1   Started                                                          0.6s
 ✔ Container task5-portainer-1  Running                                                          0.0s
roman@devops-24-4:~/tmp/netology/docker/task5$ docker image ls custom-nginx
REPOSITORY     TAG       IMAGE ID       CREATED      SIZE
custom-nginx   1.0.0     3cf8b44ba901   3 days ago   133MB
roman@devops-24-4:~/tmp/netology/docker/task5$ docker tag custom-nginx:1.0.0 localhost:5000/custom-nginx:latest
roman@devops-24-4:~/tmp/netology/docker/task5$ docker push localhost:5000/custom-nginx:latest
The push refers to repository [localhost:5000/custom-nginx]
069d96b6e2c0: Pushed
d47e4d19ddec: Pushed
8e58314e4a4f: Pushed
ed94af62a494: Pushed
875b5b50454b: Pushed
63b5f2c0d071: Pushed
d000633a5681: Pushed
latest: digest: sha256:f4cae5547d9173af9f6adcaca2eac9311be8572eba71f8b4b20c539a2141b615 size: 1777
roman@devops-24-4:~/tmp/netology/docker/task5$ curl -s http://127.0.0.1:5000/v2/_catalog
{"repositories":["custom-nginx"]}
roman@devops-24-4:~/tmp/netology/docker/task5$ curl -s http://127.0.0.1:5000/v2/custom-nginx/tags/list
{"name":"custom-nginx","tags":["latest"]}
roman@devops-24-4:~/tmp/netology/docker/task5$ docker pull localhost:5000/custom-nginx:latest
latest: Pulling from custom-nginx
Digest: sha256:f4cae5547d9173af9f6adcaca2eac9311be8572eba71f8b4b20c539a2141b615
Status: Image is up to date for localhost:5000/custom-nginx:latest
localhost:5000/custom-nginx:latest
roman@devops-24-4:~/tmp/netology/docker/task5$ docker run -d --name from-local-reg -p 127.0.0.1:8084:80 localhost:5000/custom-nginx:latest
5c0d3da32d3cfc41f97a6aaa0c31c8cef8401c6758b0ea834fae3f4df8d1508f
roman@devops-24-4:~/tmp/netology/docker/task5$ curl -s http://127.0.0.1:8084 | head -n 5
<html>
<head>
Hey, Netology
</head>
<body>
roman@devops-24-4:~/tmp/netology/docker/task5$ docker compose down
WARN[0000] Found multiple config files with supported names: /home/roman/tmp/netology/docker/task5/compose.yaml, /home/roman/tmp/netology/docker/task5/docker-compose.yaml
WARN[0000] Using /home/roman/tmp/netology/docker/task5/compose.yaml
WARN[0000] /home/roman/tmp/netology/docker/task5/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
WARN[0000] /home/roman/tmp/netology/docker/task5/compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
[+] Running 3/3
 ✔ Container task5-portainer-1  Removed                                                          0.1s
 ✔ Container task5-registry-1   Removed                                                          0.2s
 ✔ Network task5_default        Removed                                                          0.1s
roman@devops-24-4:~/tmp/netology/docker/task5$ docker compose -f docker-compose.yaml up -d
WARN[0000] /home/roman/tmp/netology/docker/task5/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
[+] Running 2/2
 ✔ Network task5_default       Created                                                           0.0s
 ✔ Container task5-registry-1  Started                                                           0.3s
roman@devops-24-4:~/tmp/netology/docker/task5$ docker compose -f docker-compose.yaml ps
WARN[0000] /home/roman/tmp/netology/docker/task5/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
NAME               IMAGE        COMMAND                  SERVICE    CREATED          STATUS          PORTS
task5-registry-1   registry:2   "/entrypoint.sh /etc…"   registry   38 seconds ago   Up 38 seconds   0.0.0.0:5000->5000/tcp, [::]:5000->5000/tcp
roman@devops-24-4:~/tmp/netology/docker/task5$ curl -s http://127.0.0.1:5000/v2/
{}roman@devops-24-4:~/tmp/netology/docker/task5$ docker compose -f docker-compose.yaml down
WARN[0000] /home/roman/tmp/netology/docker/task5/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
[+] Running 2/2
 ✔ Container task5-registry-1  Removed                                                           0.1s
 ✔ Network task5_default       Removed                                                           0.1s
roman@devops-24-4:~/tmp/netology/docker/task5$ docker compose -f compose.yaml up -d
WARN[0000] /home/roman/tmp/netology/docker/task5/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
WARN[0000] /home/roman/tmp/netology/docker/task5/compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
[+] Running 3/3
 ✔ Network task5_default        Created                                                          0.1s
 ✔ Container task5-portainer-1  Started                                                          0.3s
 ✔ Container task5-registry-1   Started                                                          0.4s
roman@devops-24-4:~/tmp/netology/docker/task5$ docker compose -f compose.yaml ps
WARN[0000] /home/roman/tmp/netology/docker/task5/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
WARN[0000] /home/roman/tmp/netology/docker/task5/compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
NAME                IMAGE                           COMMAND                  SERVICE     CREATED         STATUS         PORTS
task5-portainer-1   portainer/portainer-ce:latest   "/portainer"             portainer   7 seconds ago   Up 6 seconds
task5-registry-1    registry:2                      "/entrypoint.sh /etc…"   registry    7 seconds ago   Up 6 seconds   0.0.0.0:5000->5000/tcp, [::]:5000->5000/tcp
roman@devops-24-4:~/tmp/netology/docker/task5$ docker compose -f compose.yaml down
WARN[0000] /home/roman/tmp/netology/docker/task5/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
WARN[0000] /home/roman/tmp/netology/docker/task5/compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
[+] Running 3/3
 ✔ Container task5-portainer-1  Removed                                                          0.1s
 ✔ Container task5-registry-1   Removed                                                          0.2s
 ✔ Network task5_default        Removed                                                          0.1s
roman@devops-24-4:~/tmp/netology/docker/task5$

