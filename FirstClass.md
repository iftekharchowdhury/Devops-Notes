# Docker Basic Networking 
# Dockerfile Basic

# NetWork Interface 
## Kernel space
## User space



A network interface is the point of interconnection between a computer and a private or public network. It doesn't have a physical form.

Network Interface Card(NIC): <br/>
https://www.youtube.com/watch?v=778rS_FMb10&ab_channel=thenewboston
https://www.youtube.com/watch?v=FwNRb6MwXTI&ab_channel=freeCodeCamp.org

NIC is communication medium where ethernet one that connects to my computer and another one that connects to a communication media which is ethernet plug. 

**How do computer talk another computer: NIC** <br/>

without NIC a computer can't connect with internet. It is a circuit board installed in a computer that provides a dedicated network connection to the computer.

NIC is both a physical layer and a data link layer device

Two types of NIC cards:
1. Internal Network card 2.External Network cards.

In internal networks cards, motherboard has a slot for the network card where it can be inserted. It requires network cables to provide network access.

> Where network packet comes and go

there is a server. Packet comes from internet. Packet first goes to kernel space.

Then packet goes to User space

> What is kernal space & User space?

https://unix.stackexchange.com/questions/87625/what-is-difference-between-user-space-and-kernel-space

**Kernel space**: Kernel space is where the kernel (i.e., the core of the operating system) executes (i.e., runs) and provides its services.<br/>


Kernel work: resource manage 
### What is Kernel?<br/>
Just a computer program.basically manages operations of memory and CPU time.

- It acts as a bridge between applications and data processing done at the hardware level. It is the central component of an OS.

What is Kernel Panics?




The major aim of kernel is to manage communication between software i.e. user-level applications and hardware i.e., CPU and disk memory.

It is the computer program that first loaded on start-up the system (After the bootloader). Once it is loaded, it manages the remaining start-ups. It also manages memory, peripheral, and I/O requests from software. Moreover, it translates all I/O requests into data processing instructions for the CPU. It manages other tasks also such as memory management, task management, and disk management.

A kernel is kept and usually loaded into separate memory space, known as protected Kernel space. It is protected from being accessed by application programs or less important parts of OS.



The Kernel is responsible for low-level tasks such as disk management, memory management, task management, etc. It provides an interface between the user and the hardware components of the system. When a process makes a request to the Kernel, then it is called System Call.


**User space**: Software application where runs.Other application programs such as browser, word processor, audio & video player use separate memory space known as user-space.

NIC: Network Interface card

Layer 2 : Data link layer: MAC address niye kaj hoy. Switch

Gateway:

DHCP Server: automatic ip assign
Switch range: 171.17.0.1

DHCP uses two types of databases: network tables and a dhcptab configuration macros table. These databases are NIS+ tables if you are using NIS+, or files if you are not using NIS+.

cam table: Content Addressable Memory 

Packet Payload: 
source ip, destination ip

System call
LAN


Layer 3: 



DHCP: Dynamic HOST Configuration Protocol
A DHCP server automatically assigns a computer an:
- ip address, 
- Subnet mask,
- Default Gateway,
- DNS server

Network Packet:
Network packets are made up of three different parts, 
1. the header, 
2. the payload and 
3. the trailer. 
Network packets can be thought of conceptually to postal packages. The header is the box/envelope, the payload is the box/envelope's content, and the trailer is the signature.


`docker ps`
<br/>
`docker ps --all` 
<br/>
`docker create hello-world`<br/>
`dockert start -a hello-world id`
`docker system prune `<br/>
`docker logs container id` 
`Stopping containers - docker stop container id (only process stop )`<br/>
`kill container - docker kill container id(full container all process shutdown)`

execute an additional command in a container 

`docker exec -it container id command `<br/>

- it = allow us to provide input to the container <br/>

without -it flag nothing is happened.
1. -i = standard in <br/>
2. -t = nicely formatted text <br/>
docker exec -i id command 

Getting a command prompt in a container - <br/>

`docker exec -it container id sh` <br/>

it will give a linux command line/terminal environment
- control-D to exit

- **sh - a program which is executed inside that computer**

`docker run -it busybox sh` <br/>

- container isolation -
- suppose you open and run two containers
- docker run -it busybox sh (2 times)
now first terminal create a file 
`touch hi`
- ls - you will see the file hi
go to second terminal and check the second container and 
there is no hi file.

Every container have seperate from each other.

# Building custom images through Docker server
================================================
### CREATING DOCKER IMAGES 
<br/>
<code> <br/>
FROM alpine - Download alpine image<br/>
RUN apk add --update redis<br/>
RUN apk add --update gcc<br/>
CMD ["redis-server"]<br/>
</code>

**writing a dockerfile == told computer without os install google chrome**

**Dockerfile is a configuration file how our Docker should behave.**

`docker build .` <br/>


create a django web app<br/>
create a dockerfile
building image from Dockerfile<br/>
run image as container 
connect to web app from a browser<br/>

```
docker pull nginx:latest
docker run -p 80:80 nginx
docker rm container id
docker ps -a
docker run -d -p 80:80 -v ~/nginx-html:/usr/share/nginx/html --name my-nginx nginx

```
/usr/share/nginx/html   

The path meanings:

```

/ is the root of the current drive;
./ is the current directory;
../ is the parent of the current directory.

```

docker build -t my-nginx .

docker run -p 80:80 my-nginx

docker rm -vf $(docker ps -a -q)