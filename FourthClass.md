# Nginx - Layer 4 load Balancer

<blockquote>
NGINX is a web server that can be used as a reverse proxy, a load-balancer, a mail proxy, or an HTTP cache. It can be deployed in your local machine or in any cloud.<br>

Load balancing refers to efficiently distributing network traffic across multiple backend servers.
TCP is the protocol for many popular applications and services, such as LDAP, MySQL, and RTMP.

## Configuring Reverse Proxy

First, you will need to configure reverse proxy so that NGINX Plus or NGINX Open Source can forward TCP connections or UDP datagrams from clients to an upstream group or a proxied server.<br>

## Configuring TCP or UDP Load Balancing

Create a group of servers, or an upstream group whose traffic will be load balanced. Define one or more upstream {} configuration blocks in the top‑level stream {} context and set the name for the upstream group, for example, stream_backend for TCP servers and dns_servers for UDP servers.<br>

> Populate the upstream group with upstream servers.
> Within the upstream {} block, add a server directive for each upstream server, specifying its IP address or hostname (which can resolve to multiple IP addresses) and an obligatory port number.
> Round Robin – By default, NGINX uses the Round Robin algorithm to load balance traffic, directing it sequentially to the servers in the configured upstream group. Because it is the default method, there is no round‑robin directive; simply create an upstream {} configuration block in the top‑level stream {} context and add server directives as described in the previous step.
> Least Connections  – NGINX selects the server with the smaller number of current active connections.


## What does upstream mean in nginx?

It's used for proxying requests to other servers.<br>

Upstream is a module used in NGINX to define the servers to be load balanced. <br>

When configuring NGINX, you need to define servers for load balancing or proxying. The servers defined in an upstream are referred to by proxy_pass, fastcgi_pass, uwsgi_pass, scgi_pass, memcached_pass, and grpc_pass directives in a server.

## Here is my upstream block i set up at Nginx 

I am using two service: one is external and another one is internal. They both deploy at container.
Both have ip address. 

> External ip address: 172.17.0.3:8081
> Internal ip address: 172.17.0.4:8082

I made a Dockerfile for Nginx. I build the file and run the Nginx server 80 port.

Then i also build the external and internal Dockerfile. Then just run the both container 

`docker run -d external`
`docker run -d internal`

Then i go to the Nginx container using this command `docker exec -it nginx container id`

go to - `cd /etc/nginx/conf.d` folder

1. create a file - default.conf
2. write this code 

here stream_backend block i define my two container ip address. By default round robin algo used.<br>

**stream_backend** is the name of the upstream. Inside the server block, the traffic is routed to the upstream using pass_proxy directive. This is the basic scenario that happens inside an NGINX configuration file.

1. server
The server directive is used to define servers in an upstream. A server is defined as server the space and the server name. This is NOT the same server block defined after the upstream block.<br>

The address can be specified as a domain name or IP address, with an optional port, or as a UNIX-domain socket path specified after the “unix:” prefix. If a port is not specified, the port 80 is used. 

2. weight
By default, requests are distributed between the servers using a weighted round-robin balancing method. weight directive configs the load weight of a server. By default it's 1. weight is used as weight=number. Let me explain it with an example.

```
upstream backend {
    server backend1.example.com       weight=3;
    server backend2.example.com;
    server backend3.example.com;
}

```


```
upstream <upstream_name> {
   server <server_name>
}

```
According to this example, if 5 requests come to the upstream, the first 3 requests are sent to the first server which is backend1.example.com and accordingly one request each for the other two servers. This is basically the same as traffic shifting.<br>

3. max_conns
This configuration limits the maximum number of connections the server can connect. By default, this value is zero, which is unlimited connections. If the server group does not reside in the shared memory, the limitation works per each worker process.<br/>

4. max_fails
As I mentioned above, when a request comes to an upstream server, if the server is not available, it waits till the server is up and running, or if not it goes to the next server. Using max_fails the directive, you can set the number of unsuccessful attempts to communicate with the server that should happen in the duration set by the fail_timeout to consider the server unavailable for a duration also set by the fail_timeout parameter.
The default value of max_fails is 1. The zero value disables the accounting of attempts. A proxy unsuccessful attempt is an attempt where the proxy could not connect to the server due to a server internal error, lost connection, server unavailability etc.<br>

5. fail_timeout

This parameter sets, the time during which the specified number of unsuccessful attempts to communicate with the server should happen to consider the server unavailable; and the period of time the server will be considered unavailable.
By default, the parameter is set to 10 seconds.<br/>

6. backup<br/>


When you need to use one or many servers as a backup, you can use the directive backup so when the request pass to this server only when the primary servers are unavailable.

```
upstream backend {
    server backend1.example.com;
    server backend2.example.com;
    server backend3.example.com backup;
}
```
7. down
This directive is used to mark servers as temporarily unavailable.

```
upstream <upstream_name> {
   
}

```


```
stream{
        upstream stream_backend {
                server 172.17.0.3:8081;
                server 172.17.0.4:8082;
}

server {

    listen       8081;
    #listen  [::]:8081;
    #root    /usr/share/nginx/html;
    proxy_pass stream_backend;


}

}


```

But there is a issue a faced. Here it is:

# nginx: [emerg] “stream” directive is not allowed here

i found the solution. I couldn't understand. Then second time actually understand.

I checked the nginx.conf file and there is http block. In this block, there is line 

`include /etc/nginx/conf.d/*.conf;` <br>

I just took the line and throw it outside of the http block. Problem solved :cheers:

When you changed anything in server configuration file you need to restart. But i don't know how to restart nginx docker container. I figured it out bro :cheers:

## How to restart docker nginx container

**`docker exec container id nginx -s reload`**

Then, I use tcpdump and check out the network packet movement. I go to nginx container 
and check the packet movement.

## how to check docker container logs to solve issue?

`docker logs container id`

This helps me to solve my nginx container issue. Very helpful to identifying issue.


</blockquote>
