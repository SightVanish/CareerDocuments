# Docker Tips

1. Pull docker images `docker pull docker.io/library/ubuntu:18.04` or `docker pull ubuntu:18.04` in short (from docker hub)

2. Test docker

    1. `docker run -it --rm ubuntu:18.04 bash`, `-it` stands for interactive terminal, `--rm` stands for remove after exiting this container, `bash` is the shell we use in container.
    2. `cat /etc/os-release` show system info

3. List docker images `docker images`

4. `docker run -dit ubuntu:18.04` --run a docker in background with interactive pseudo terminal (not assigned)

    `docker container ls` --find your running container

    `docker exec -i <container id> bash` --enter container via bash

    `exit` in this bash will not stop docker

    `docker container stop <container id>`--stop container

5. `docker container ls -a` --list all containers, including stopped container

    `docker container rm <container id>` --remove a stopped container

    `docker container prune` --remove all stopped container