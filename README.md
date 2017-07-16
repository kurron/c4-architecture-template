# Overview
This image is designed to be used by CI/CD systems and developers that need to
build JVM projects from within Docker.  The container is designed to
not only allow for compilation of JVM projects but also the assembly and
deployment of Docker images and containers.  In addition, Ansible is
available to orchestrate the tests. If you are looking for something to
[run a JVM application, try this](https://github.com/kurron/docker-azul-jdk-8).

# Prerequisites
* a working [Docker](http://docker.io) engine
* a working [Docker Compose](http://docker.io) installation

# Building
Type `./build.sh` to build the image.

# Installation
Docker will automatically install the newly built image into the cache.

# Tips and Tricks

## Launching The Image
Use `./test.sh` to exercise the image.  A couple commands to try:

1. `./test.sh` 
1. `./test.sh java -version` 
1. `./test.sh docker info` 
1. `./test.sh docker-compose --version` 
1. `./test.sh ansible --version` 
1. `./test.sh ansible all --inventory='localhost,' --connection=local -m ping` 

## Examples
There is an `examples` folder that has samples on how to run `Gradle`,
run an `Ansible` playbook, create and tag a `Docker` image.

## Controlling Docker From Inside The Container
If you need to run docker commands from inside your container, you will need
to add a mount to the Docker daemon at container launch time.  Here is an
example of the `docker run` switch needed:

`--volume /var/run/docker.sock:/var/run/docker.sock`

In addition to the mount, you will also have to add the container to
the `docker` group or you will get permission errors when trying to access the Docker
daemon. Here is an example of the `docker run` switch needed:

`--group-add ${DOCKER_GROUP_ID}`

The Docker group id can be found via `cut -d: -f3 < <(getent group docker`. Another
option is to run as the `root` user, which is a security risk.

## Running Ansible From Inside The Container
Nothing special needs to be done to run Ansible.  As long as the playbook is mounted in th
container, then things should work as expected.  When having Ansible run commands locally
make sure to **specify a local connection** or Ansible will attempt to establish an SSH connection,
which will fail. No SSH server is running in the container. The command-line switch to use:

`ansible-playbook --inventory='localhost,' --verbose --connection=local playbook.yml`

You can also specify in the playbook itself.

```
---
- hosts: localhost
  connection: local

  tasks:
    - name: Build Docker Image
      command: "docker-compose --verbose build"
```


# Troubleshooting

## User and Group IDs
The image contains a non-root user named `powerless` that is bound to ids of`1000:1000`
which matches the default ids of many Linux distributions.  This was done, in addition
to security concerns, to allow any output of builds to be owned by the host's account.
It isn't any fun if your newly compiled can only be accessed by `root`!  This can
cause complications with `Ansible` if the host account uses different ids, preventing
Ansible from running.  Currently, the only known work around is to build your own
image and add in an additional non-root account that uses your ids.

# License and Credits
This project is licensed under the
[Apache License Version 2.0, January 2004](http://www.apache.org/licenses/).

* [Guidance for Docker Image Authors](http://www.projectatomic.io/docs/docker-image-author-guidance/)
* [Java RAM Usage in Containers: Top 5 Tips Not to Lose Your Memory](http://blog.jelastic.com/2017/04/13/java-ram-usage-in-containers-top-5-tips-not-to-lose-your-memory/)
* [Java and Memory Limits in Containers: LXC, Docker and OpenVZ](http://blog.jelastic.com/2016/05/03/java-and-memory-limits-in-containers-lxc-docker-and-openvz/)
* [OpenJDK and Containers](https://developers.redhat.com/blog/2017/04/04/openjdk-and-containers/)
* [Java VM Options You Should Always Use in Production](http://blog.sokolenko.me/2014/11/javavm-options-production.html)
* [Exec form ENTRYPOINT example](https://docs.docker.com/engine/reference/builder/#exec-form-entrypoint-example)
* [Java SE support for Docker CPU and memory limits](https://blogs.oracle.com/java-platform-group/java-se-support-for-docker-cpu-and-memory-limits)

# List of Changes

* OpenJDK Runtime Environment (Zulu 8.21.0.1-linux64) (build 1.8.0_131-b11)
* Docker version 17.03.2-ce, build f5ec1e2
* docker-compose version 1.14.0, build c7bdf9e
* ansible 2.3.1.0
