# Disposable development environment with Docker

Inspired by Fedora Toolbox, this tool allows you to use a docker container to create a disposable environment for a specific task, while keeping things clean on the real os.

The tool provides a shell to the environment with the same local user and groups, and with access to the current directory (and optionally the whole home directory). 

It's then possibile to install packages on the container and do some work, everything is kept through multiple sessions; then, when finished, the environment can be deleted with eveything in it.

## Create a new environment

```
docker-env create test123
```

## Use an environment

```
docker-env enter test123
```

The current directory is mounted in `/project` but is also possible to mount the whole user home directory.

The same environment can be used multiple times without losing any data, as the modified image is committed on exit

## Delete the enviroment

```
docker-env remove test123
```

## Usage

```
Usage: docker-env command [options] name

Commands:
  create      Create the docker image
  enter       Run the docker container and opens a shell
  remove      Delete the docker container and image

Options:
  create 
   -i, --base-image  IMAGE   Set the base docker image to use to build the image, default 'debian:stable-slim'
   -p, --password PASS       Set the root password, default 'docker'
  enter 
   -h, --host HOST           Set the host name, default 'docker-host'
   -m, --mount-home          Mount the real home folder to the environment home folder

Other:	
  The current folder is always mounted in /project
```

## Example
```
user@local:~/somewhere$ docker-env create -i debian:stretch stretch-env
user@local:~/somewhere$ docker-env enter stretch-env
user@docker-host:/project$
... do work ...
user@docker-host:/project$ exit
user@local:~/somewhere$ docker-env remove stretch-env
```

## Notes
Based on debian, to work with other distros the script may require changes.
Works on both Linux and macOS.