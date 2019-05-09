# DOCKER IN GENERAL
Good articles:
- Part 1: https://towardsdatascience.com/learn-enough-docker-to-be-useful-b7ba70caeb4b
- Part 2: https://towardsdatascience.com/learn-enough-docker-to-be-useful-1c40ea269fa8
- Part 3: https://towardsdatascience.com/learn-enough-docker-to-be-useful-b0b44222eef5
- Part 4: https://towardsdatascience.com/slimming-down-your-docker-images-275f0ca9337e
- Part 5: https://towardsdatascience.com/15-docker-commands-you-should-know-970ea5203421
- Part 6: https://towardsdatascience.com/pump-up-the-volumes-data-in-docker-a21950a8cd8

overview:
https://docs.docker.com/engine/docker-overview/

what is bind data:
https://unix.stackexchange.com/questions/198590/what-is-a-bind-mount

## First simple app (Linux vs WIN10 Home)
First simple docker with small Python code:
https://medium.freecodecamp.org/a-beginners-guide-to-docker-how-to-create-your-first-docker-application-cc03de9b639f
COMMENT: this example works on Linux with no problem.
On WIN10 it returns error that it cannot find the file Dockerfile

I used following commands:
```
docker build -t python-test .

docker run python-test

docker stop python-test
```


## Second  simple app (Linux vs WIN10 Home)
https://www.wintellect.com/containerize-python-app-5-minutes/ 
I used following commands:
```
docker build --tag my-python-app .

docker run --name python-app -p 5000:5000 my-python-app

docker stop second-python-test
```

## Third py docker app
https://djangostars.com/blog/what-is-docker-and-how-to-use-it-with-python/


# DOCKER FOR LINUX

## INSTALLATION:
- to install docker on linux use sudo install. select based on your system prerequisites
https://docs.docker.com/install/linux/docker-ce/ubuntu/







# DOCKER FOR WINDOWS:
That is not always good idea - read: https://medium.com/devopslinks/hey-docker-why-you-hate-windows-so-much-de7a7aa4dd7
MAIN problems:
- I cannot make docker volumes up and running
(READ: https://stackoverflow.com/questions/34161352/docker-sharing-a-volume-on-windows-with-docker-toolbox)
- My VPN software is making some issues with containers
Volume or network command in docker-compose is just not working
- I have some issues with Windows 7/8/10+
- I am using a Corporate VPN (like PulseSecure or other jewels) which is making some weird issues with networking
- I would love to play with Kubernetes but (see points above)
- and more …
## INSTALLATION:
because I do not have WIN 10 Pro, I have to install Toolbox for docker
As part of installation was also Oracle Virtual Machine box and Kitematic
https://docs.docker.com/docker-for-windows/install/

### PROBLEMS:
I wanted to run in PowerShell following commands:
```
$ docker --version 
```
- it worked
```
$ docker ps 
```
- failed (returns error that it cannot connect and that docker daemon is probably not running )
- we tried to run this command in WindowsPowerShell and with cmd - did not work
- NOTE: Open a terminal window (Command Prompt or PowerShell, but not PowerShell ISE)
- we open Oracle VM Box to check if Virtual Machine is running. We started one box, tried $docker ps .. got same error.
- then we tried with Kitematic (https://kitematic.com/ or https://docs.docker.com/kitematic/userguide/). It is very useful tool when learning Dockers and has nice GUI. We successfully ran few open source dockers.
--> at the bootom of Kitematic app, we see DOCKER CLI. opens similar WindowsPowerShell. Here all following commands work

Another problem - Kitematic did not start and was showing error
```
ENOENT for ca.pem #1008
```
this solution worked:
https://github.com/docker/kitematic/issues/1008  
- Do you have a properly created certificate? If yes, you can re-generate the certificates for your VM via:
```
docker-machine -D regenerate-certs default
```

## FIRST TEST
(source of tut: https://docs.docker.com/docker-for-windows/)
1. Pull the hello-world image from Docker Hub and run a container:
```
$ docker run hello-world
```
2. List the hello-world image that was downloaded from Docker Hub:
```
$ docker image ls
```
3. List the hello-world container (that exited after displaying “Hello from Docker!”):
```
$ docker container ls --all
```
4. Explore the Docker help pages by running some help commands:
```
$ docker --help  all available commands for docker)
$ docker container --help  (all available commands for container)
$ docker container ls --help
$ docker run --help (all available commands that can be used when running dockers)
$ docker container ls --all
```
## EXPLORE the APPLICATION
1. Pull an image of the Ubuntu OS and run an interactive terminal inside the spawned container:
```
$ docker run --interactive --tty ubuntu bash
```
- it works OK
2. You are in the container. At the root # prompt, check the hostname of the container:
```
# hostname
```
Notice that the hostname is assigned as the container ID (and is also used in the prompt).

3. Exit the shell with the exit command (which also stops the container):
```
# exit
```
4. List containers with the --all option (because no containers are running)
```
$ docker container ls --all
```
5. Pull and run a Dockerized nginx web server that we name, webserver
```
$ docker run --detach --publish 80:80 --name webserver nginx
```




### DOCKERFILE instructions
```
FROM — specifies the base (parent) image.
LABEL —provides metadata. Good place to include maintainer info.
ENV — sets a persistent environment variable.
RUN —runs a command and creates an image layer. Used to install packages into containers.
COPY — copies files and directories to the container.
ADD — copies files and directories to the container. Can upack local .tar files.
CMD — provides a command and arguments for an executing container. Parameters can be overridden. There can be only one CMD.
WORKDIR — sets the working directory for the instructions that follow.
ARG — defines a variable to pass to Docker at build-time.
ENTRYPOINT — provides command and arguments for an executing container. Arguments persist. 
EXPOSE — exposes a port.
VOLUME — creates a directory mount point to access and store persistent data.
```
DockerFile reference: https://docs.docker.com/engine/reference/builder/
