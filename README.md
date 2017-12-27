Kick-Start

What is Docker?

- Docker by Docker Official Website :
  Docker is the company driving the container movement and the only container platform provider to address every application across the hybrid cloud. Today’s businesses are under pressure to digitally transform but are constrained by existing applications and infrastructure while rationalizing an increasingly diverse portfolio of clouds, datacenters and application architectures. Docker enables true independence between applications and infrastructure and developers and IT ops to unlock their potential and creates a model for better collaboration and innovation.

- Docker by Wikipedia
  an open-source project that automates the deployment of software applications inside containersby providing an additional layer of abstraction and automation of OS-level virtualization on Linux.
- In summary:
  docker is an open-source project that use OS-level virtualization technology to provide an isolated context called container to run application without overheads of virtual machines technology that used tereditionally!

in few next paragraphs we will talk about virtualization technology!you can jump to Docker Hello World if you are not intrest!



Virtualization history

Virtualization is a broad concept that refers to the creation of a virtual version of something, whether hardware, a software environment, storage, or a network.

In a virtualized environment there are three major components:

- Guest: represents the system component that interacts with the virtualization layer rather than with the host, as would normally happen
- Host: represents the original environment where the guest is supposed to be managed
- Virtualization layer: is responsible for recreating the same or a different environment where the guest will operate

Pre-Virtualization World

day 0, you're alone, no virtual machines , no hypervisor hole damn resources is yours!each application run on a dedicated server with a host OS.

- benefits:
  - no overhead!
  - security
  - full and total access to its resources
  - performs an extremely high volume of read and/or write actions to the hard disk 
- disadvantage:
  - waste of money
  - waste of energy
  - waste of resource
  - no elasticity
  - no scalability
  - slow deploy
  - hard to migrate
    

Hypervisor-based Virtualization

i believe that God sent hypervisors to save our lives!The hypervisor or virtual machine manager (VMM) is generally a program or a combination of software and hardware that allows the abstraction of the underlying physical hardware.

there are two major types of hypervisor :

- Type I hypervisors (native virtual machine) run directly on top of the hardware
  - Therefore, they take the place of the operating systems and interact directly with the ISA interface exposed by the underlying hardware, and they emulate this interface in order to allow the management of guest operating systems

- Type II hypervisors (hosted virtual machines) require the support of an operating system to provide virtualization services
  - This means that they are programs managed by the operating system, which interact with it through the ABI and emulate the ISA of virtual hardware for guest operating systems 

Moreover, virtualization technologies provide a virtual environment for not only executing applications but also for storage, memory, and networking





- benefits:
  - pay as need 
  - cost efficient 
  - security(isolated context for deploying applications)
  - energy efficient
  - migration
  - easy to scale
    
- disadvantage:
  - long boot time
  - hard to migrate
  - overhead
  - slow deploy
  - security(opens the door to a new and unexpected form of phishing)
    

container-based Virtualization

Container virtualization (often referred as operating system virtualization) is more than just a different kind of hypervisor. Containers use the host operating system as their base, and not the hypervisor. Rather than virtualizing the hardware (which requires full virtualized operating system images for each guest), containers virtualize the OS itself, sharing the host OS kernel and its resources with both the host and other containers.





- benefits:
  - pay as you need
  - elasticity
  - scalibility
  - fast deployment
  - easy to migrate
  - less overhead
  - fast boot 
  - energy efficient
  - consistent environment
  - layered filesystem
  
- disadvantage:
  - Containers don't run at bare-metal speeds. Containers consume resources more efficiently than virtual machines. But containers are still subject to performance overhead due to overlay networking, interfacing between containers and the host system and so on. If you want 100 percent bare-metal performance, you need to use bare metal, not containers.
  - Persistent data storage is complicated. By design, all of the data inside a container disappears forever when the container shuts down, unless you save it somewhere else first. There are ways to save data persistently in Docker, such as Docker Data Volumes, but this is arguably a challenge that still has yet to be addressed in a seamless way.
  - Graphical applications don't work well. Docker was designed as a solution for deploying server applications that don't require a graphical interface. While there are some creative strategies (such as X11 video forwarding) that you can use to run a GUI app inside a container, these solutions are clunky at best.
  - Not all applications benefit from containers. In general, only applications that are designed to run as a set of discreet microservices stand to gain the most from containers. Otherwise, Docker's only real benefit is that it can simplify application delivery by providing an easy packaging mechanism.

Docker Performance and architecture

Architecture

Docker uses a client-server architecture. The Docker client talks to the Docker daemon, which does the heavy lifting of building, running, and distributing your Docker containers. The Docker client and daemon can run on the same system, or you can connect a Docker client to a remote Docker daemon. The Docker client and daemon communicate using a REST API, over UNIX sockets or a network interface.



Docker on Linux

On Linux systems, Docker directly leverages the kernel of the host system, and file system mounts are native. (home sweet home)



Docker on WIndows

 In Docker for Windows does each container run in separate VM?



There are two types of Windows containers... Windows Containers & Hyper-V Containers. Windows Containers work the same way you know Linux based containers work... one or more in a host where the host can be a VM. Hyper-V containers are different though in that they run a single container within a tiny Hyper-V VM.

We interviewed the guy who owns the Windows Container story for Microsoft recently on our podcast if you're interested in learning not only more about this, but where they are going & helping. I found it fascinating how much an old engineering team like Windows is contributing to an open source project!

http://www.microsoftcloudshow.com/podcast/Episodes/137-windows-containers-are-coming-talking-to-taylor-brown-about-the-container-wave-coming-to-the-microsoft-world480



Docker on Mac

In June 2016 Docker announced Docker for Mac. The “new” way to run Docker on Mac with much easier installation and a more Linux-y experience for Docker users. Docker for Mac still starts a virtual machine (even though it is super hidden). It also brought its own hypervisor hyperkit and shared file system osxfs. Unfortunately, “osxfs” wasn’t very fast, and from the beginning there have been long discussions about it (Docker, Github).

Docker has steadily been working on performance improvements for Docker for Mac and released improvements with 17.04 CE. 17.04 CE now brings new performance flags to mountpoints of Docker Volumes (“delegated” and “cached”). Docker talks about an 2x — 3.5x improvement when comparing Docker for Mac 17.04 CE vs older versions.



Hello World

now we'll run our first docker image and create a new container:

    docker run hello-world

and the result is:

    Unable to find image 'hello-world:latest' locally
    docker: Error response from daemon: error parsing HTTP 403 response body: invalid character '<' looking for beginning of value: "<html><body><h1>403 Forbidden</h1>\nSince Docker is a US company, we must comply with US export control regulations. In an effort to comply with these, we now block all IP addresses that are located in Cuba, Iran, North Korea, Republic of Crimea, Sudan, and Syria. If you are not in one of these cities, countries, or regions and are blocked, please reach out to https://support.docker.com\n</body></html>\n\n".
    See 'docker run --help'.

lets see what happend! read the first line of output,we have diffrent scenario when we run a docker image:

- scenario 1
  after you try tu run hello-world image, docker search for this image on your local machine,if its stored there from befor, new container create from image will be create and sart
- scenario 2
  but what if docker cant find image locally?if you're not connected from Iran, North Korea, Republic of Crimea, Sudan, and Syria, in this scenario docker should search on an online repository to find this image!this repositories called Registery! after finding image docker will pull this requested image to your local machine storage and start your image to create new container
  but if you're a citizen of banned regions probeblly you will see this error:
      docker: Error response from daemon: error parsing HTTP 403 response body: invalid character '<' looking for beginning of value: "<html><body><h1>403 Forbidden</h1>\nSince Docker is a US company, we must comply with US export control regulations. In an effort to comply with these, we now block all IP addresses that are located in Cuba, Iran, North Korea, Republic of Crimea, Sudan, and Syria. If you are not in one of these cities, countries, or regions and are blocked, please reach out to https://support.docker.com\n</body></html>\n\n".
      See 'docker run --help'.
  ok all you need is a VPN!

ok lets try again:

    makbns-MacBook-Pro:~ makbn$ docker run hello-world
    Unable to find image 'hello-world:latest' locally
    latest: Pulling from library/hello-world
    ca4f61b1923c: Pull complete 
    Digest: sha256:445b2fe9afea8b4aa0b2f27fe49dd6ad130dfe7a8fd0832be5de99625dad47cd
    Status: Downloaded newer image for hello-world:latest
    
    Hello from Docker!
    This message shows that your installation appears to be working correctly.
    
    To generate this message, Docker took the following steps:
     1. The Docker client contacted the Docker daemon.
     2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
        (amd64)
     3. The Docker daemon created a new container from that image which runs the
        executable that produces the output you are currently reading.
     4. The Docker daemon streamed that output to the Docker client, which sent it
        to your terminal.
    
    

docker couldn't find image locally then tries to download it from registery!after download finished, image saved locally and stared by docker deamon!

- Where are Docker images stored on the host machine?



Docker objects

When you use Docker, you are creating and using images, containers, networks, volumes, plugins, and other objects. This section is a brief overview of some of those objects.

IMAGES

An image is a read-only template with instructions for creating a Docker container. Often, an image is based onanother image, with some additional customization. For example, you may build an image which is based on the ubuntu image, but installs the Apache web server and your application, as well as the configuration details needed to make your application run.

You might create your own images or you might only use those created by others and published in a registry. To build your own image, you create a Dockerfile with a simple syntax for defining the steps needed to create the image and run it. Each instruction in a Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt. This is part of what makes images so lightweight, small, and fast, when compared to other virtualization technologies.

CONTAINERS

A container is a runnable instance of an image. You can create, start, stop, move, or delete a container using the Docker API or CLI. You can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.

By default, a container is relatively well isolated from other containers and its host machine. You can control how isolated a container’s network, storage, or other underlying subsystems are from other containers or from the host machine.

A container is defined by its image as well as any configuration options you provide to it when you create or start it. When a container is removed, any changes to its state that are not stored in persistent storage disappear.



Docker Basic Commands

docker run

Run a command in a new container

    docker run [OPTIONS] IMAGE [COMMAND] [ARG...]

options

  Name, shorthand   	Default	Description                             
  --env , -e        	       	Set environment variables               
  --expose          	       	Expose a port or a range of ports       
  --rm              	       	Automatically remove the container when it exits
  --tty , -t        	       	Allocate a pseudo-TTY                   
  --interactive , -i	       	Keep STDIN open even if not attached    
  -d                	       	run in detached mode all the time       

example

    docker run -it --name ubuntu_cont ubuntu:latest bash

    docker run -it busybox:latest echo "hello world"







docker start

Start one or more stopped containers in detached mode

    docker start [OPTIONS] CONTAINER [CONTAINER...]

options

  Name, shorthand   	Default	Description             
  --interactive , -i	       	Attach container’s STDIN

example

    docker start -i ca765vb







docker ps

list of containers

    docker ps [OPTIONS]

options

  Name, shorthand	Default	Description        
  —all , -a      	       	show all containers

example

    docker ps -a







docker images

list of images

    docker images [OPTIONS] [REPOSITORY[:TAG]]

options

  Name, shorthand	Default	Description    
  —all , -a      	       	show all images

- docker image have intermediate layers that increase reusability, decrease disk usage and spped up docker build by allowing each step to be cached! these intermediat layer are not shoen by default.

example

    docker images -a





docker stop

Stop one or more running container

    docker stop [OPTIONS] CONTAINER [CONTAINER...]

options

  Name, shorthand	Default	Description                             
  —time, -t      	10     	seconds to wait for stop before killing it

example

    docker stop -t 100 34tfer 





docker kill

Kill one or more running containers

    docker kill [OPTIONS] CONTAINER [CONTAINER...]

options

  Name, shorthand	Default	Description                    
  --signal , -s  	KILL   	Signal to send to the container

- stop vs. kill?

example

    docker kill cae40c







docker exec

Run a command in a running container

    dockr exec [OPTIONS] CONTAINER [ARGS...]

options

  Name, shorthand   	Default	Description                             
  --detach , -d     	       	Detached mode: run command in the background
  --interactive , -i	       	Keep STDIN open even if not attached    
  --tty , -t        	       	Allocate a pseudo-TTY                   

- COMMAND should be an executable, a chained or a quoted command will not work. Example:
  -  docker exec -ti my_container "echo a && echo b" will not work, but 
  - docker exec -ti my_container sh -c "echo a && echo b" will.


