<div align="center">
h

<!-- add technical charcha logo postgres session 3 -->
# PostgresSQL Session 4        
### — Task Documentation by Yash Anand —    
__________________________________________________________________________________

## Contents
</div>

## Contents

  - [**Task 1: Create Roles**](#task-1-create-roles)
  - [**References**](#references)
_____________________________________________________________________________________     
<div align="center">

## **Task 1**
**What is process, share the command so that we can identify resources utilisation according to process**
</div>
In the context of our system, a process is the ongoing execution of a program. Processes handle commands and run programs and services. Every process has a process ID or pid. In docker, a process can be equated with containers, meaning that an entire container can be seen as a process. However, inside these containers as well, the services and commands being executed are also processes.

For finding processes running on our system, we can run the `top` command. But if we would like to find the processes running inside of docker/podman, we can run `docker stats`/`podman stats` or if we would like to find the processes running inside of a container, we can run `docker top <containername>`/`podman top <containername>`.
___________________________________________________

## **Task 2**
**What is pid #1 of system and pid  #1 of container**
</div>

PID or process ID is the unique identification assigned to a process, in both our system and in container. In our system, pid #1 is assigned to systemd or the first ever process that is run on the system before running any other processes. This can be found by running the `top -p 1` command, where top is a memory managing command and -p is the process. The first process that is run is the init or systemd process, which is used for managing and controling system processes.

Similarly in containers, pid 1 refers to the first process that is started with the container. In docker and podman, this process is also responsible for managing and starting a container and pid #1 can be specified in the dockerfile while creating a container. The processes running inside of a container can be found using `docker top <containername> -p <processid>`. 
___________________________________________________

## **Task 6**
**Difference between podman and docker**
</div>

Both help containerise applications. Containers help package applications, codes and runtime in a single unit that can be deployed in various environments. The differences between podman and docker are as follows

| Podman                                              | Docker                                     |
|-----------------------------------------------------|--------------------------------------------|
| Podman follows a daemonless architecture, meaning it doesn't require a long-running background service (like the Docker daemon) to manage containers. Each Podman command directly interacts with the container runtime, making it more lightweight and secure. | Docker uses a client-server architecture with a background daemon (Dockerd) that manages container operations. The client communicates with the daemon to control containers. |
| Podman makes it easy to run containers as a non-root user, offering better security and allowing users to run containers without elevated privileges. | Docker also supports rootless containers, but the setup can be more complex. |
| Podman can generate systemd service files to manage containers as services. This simplifies autostarting containers, monitoring resources, and managing containers with a status page. | Docker relies on tools like docker-compose for similar functionality, but it may require additional setup for resource monitoring and autostarting containers. |
| Podman supports the concept of "pods," which is a way to group and manage multiple containers as a single unit. This feature is similar to Kubernetes pods. | Docker also introduced pod support in later versions, but it may not be as mature as Podman's implementation. |
| Podman provides built-in support for automatic updates of containers and pods. | Docker might require external tools like Watchtower for automatic updates. |
| Podman simplifies inter-container networking, making it easier to set up and manage. | Docker handles inter-container networking, but it might require additional setup, especially in more complex network configurations. |

___________________________________________________

## **Task 7**
**Docker should be running non root user without sudo  **
</div>

Applications by default have root priveleges inside of containers which means that important changes can be made easily which is a threat to secuirty. In order to run Docker as a non-root user, we can add the user to docker group which will allow running docker without superuser priveleges. This can be done in the following steps:
- sudo groupadd docker (In my case I was already non-root)
- sudo usermod −aG docker <nonrootusername> (here 'modify user' & 'appended' him to a 'Group' of docker)
___________________________________________________

## **References**
</div>
Task 1: 
https://www.padok.fr/en/blog/docker-processes-container#:~:text=Each%20process%20can%20have%20child,you%20can%20imagine%20its%20importance.

Task 2:
https://www.reddit.com/r/docker/comments/119unid/docker_and_pid_1/

Task 7:
https://www.tutorialspoint.com/running-docker-container-as-a-non-root-user

Task 8:


--------
