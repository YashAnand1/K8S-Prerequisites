<div align="center">

<!-- add technical charcha logo postgres session 3 -->
# K8S      
### — Task Documentation by Yash Anand —    
__________________________________________________________________________________

## Contents
</div>

## Contents
- [Task 1](#task-1)
- [Task 2](#task-2)
- [Task 3](#task-3)
- [Task 6](#task-6)
- [Task 7](#task-7)
- [Task 8](#task-8)
- [References](#references)

_____________________________________________________________________________________     
<div align="center">

## **Task 1**
**What is process, share the command so that we can identify resources utilisation according to process**
</div>
In the context of our system, a process is the ongoing execution of a program. Processes handle commands and run programs and services. Every process has a process ID or pid. In docker, a process can be equated with containers, meaning that an entire container can be seen as a process. However, inside these containers as well, the services and commands being executed are also processes.

For finding processes running on our system, we can run the `top` command. But if we would like to find the processes running inside of docker/podman, we can run `docker stats`/`podman stats` or if we would like to find the processes running inside of a container, we can run `docker top <containername>`/`podman top <containername>`.
___________________________________________________

<div align="center">

## **Task 2**
**What is pid #1 of system and pid  #1 of container**
</div>

PID or process ID is the unique identification assigned to a process, in both our system and in container. In our system, pid #1 is assigned to systemd or the first ever process that is run on the system before running any other processes. This can be found by running the `top -p 1` command, where top is a memory managing command and -p is the process. The first process that is run is the init or systemd process, which is used for managing and controling system processes.

Similarly in containers, pid 1 refers to the first process that is started with the container. In docker and podman, this process is also responsible for managing and starting a container and pid #1 can be specified in the dockerfile while creating a container. The processes running inside of a container can be found using `docker top <containername> -p <processid>`. 
___________________________________________________

## **Task 3**
**Push any image on nexus repository over the SSL (443) which you have configure in question 3**
</div>

Nexus server helps host docker images. Using docker compose, we create nexus repository. We expose 3 ports: 8181 web port for accessing ui, 81 for docker hub repo, 83 for private repository. The compose file was as follows:
```
version: "3.7"

services:
  nexus:
    image: sonatype/nexus3
    expose:
      - 8081
      - 8084
      - 8083
    ports:
      - "8084:8082"
      - "8083:8083"
      - "8081:8081"
    volumes:
      - ./volume:/nexus-data
    restart: always

```
In the compose file, volume directory will be having the nexus data and before composing the repository, we run chmod 777. The output of this will create the docker container:
![img](https://i.imgur.com/kaLuROy.png)

To ensure that the server was indeed created and has started, we will run 'docker logs -f lab-nexus-sever-master_nexus_1'. The output will be:
![img](https://i.imgur.com/4Ev1Drq.png)

We can access nexus from localhost:8081 and to login, we use the 'admin' user and the password is in the '/nexus/data/admin_password'. 
![img](https://i.imgur.com/yd6r9Cl.png)

After signing in, we are asked to create a new password. After I had created a new password, I was asked to choose configure anonymous access, meaning I would not have to login to pull public images.

To create the SSL certificate, I ran 'keytool -printcert -rfc -sslserver repo1.maven.org > repo1.pem' as it had been mentioned as a method in the [Nexus documentation](https://help.sonatype.com/repomanager3/nexus-repository-administration/configuring-ssl) for connecting with SSL. Afterwards, I entered into the [admin settings](http://localhost:8081/#admin/security/sslcertificates) and pasted the certificate of the pem file that had been created earlier. 

Soon I was asked to add the certificate to truststore to complete the SSL connection process and once done, my SSL certificate was added successfuly:

![img](https://i.imgur.com/OXYhVCd.png)


___________________________________________________


<div align="center">

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

<div align="center">

## **Task 7**
**Docker should be running non root user without sudo**
</div>

Applications by default have root priveleges inside of containers which means that important changes can be made easily which is a threat to secuirty. In order to run Docker as a non-root user, we can add the user to docker group which will allow running docker without superuser priveleges. This can be done in the following steps:
- sudo groupadd docker (In my case I was already non-root)
- sudo usermod −aG docker <nonrootusername> (here 'modify user' & 'appended' him to a 'Group' of docker)
___________________________________________________

## **Task 8**
**Setup gitea on podman container and perform clone and push operation**
</div>

In order to setup gitea on podman, I ran the following command for creating a podman container
```
user@yashanand:~/gitea$ sudo podman run -d --name=gitea -p 3001:3000 -p 23:22 gitea/gitea:latest
```
Through this, I was able to successfuly create a gitea container on my system. I also visited 'localhost:3001' to further setup gitea on my system. I let the default configurations stay as they were and installed gitea:
![img](https://i.imgur.com/61YcBnh.png)

___________________________________________________

<div align="center">

## **References**
</div>
Task 1: 
https://www.padok.fr/en/blog/docker-processes-container#:~:text=Each%20process%20can%20have%20child,you%20can%20imagine%20its%20importance.

Task 2:
https://www.reddit.com/r/docker/comments/119unid/docker_and_pid_1/

Task 3:
https://www.youtube.com/watch?v=dpWxWr90MGI
https://support.sonatype.com/hc/en-us/articles/217542177-Using-Self-Signed-Certificates-with-Nexus-Repository-and-Docker-Daemon

Task 6:
https://www.imaginarycloud.com/blog/podman-vs-docker/#:~:text=Podman%20is%20different%20from%20Docker,users%2C%20which%20can%20improve%20security.

Task 7:
https://www.tutorialspoint.com/running-docker-container-as-a-non-root-user

Task 8:
https://www.digitalocean.com/community/tutorials/how-to-install-gitea-on-ubuntu-using-docker

--------
