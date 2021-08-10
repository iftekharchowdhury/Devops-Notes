# Learn and write about CIDR. About it’s calculation, network and host etc.

> **CIDR = Classless inter-domain routing**
> It is a method for allocating ip addresses and IP routing.
> CIDR first introduced by Internet Engineering task force in 1993
> Goal : slow the growth of routing tables on routers across the internet.

CIDR introduced a new method of representation for ip addresses - **knows as CIDR notation**

CIDR is based on the idea of subnet masks. A mask is placed over an IP address and creates a sub network: a network that is subordinate to the internet. The subnet mask signals to the router which part of the IP address is assigned to the hosts (the individual participants of the network) and which determines the network.

## Calculating CIDR

<blockquote>
CIDR is based on the idea of subnet masks. A mask is placed over an IP address and creates a sub network: a network that is subordinate to the internet. The subnet mask signals to the router which part of the IP address is assigned to the hosts (the individual participants of the network) and which determines the network.

The first address – the network address that shouldn’t be used – is 210.105.40.0/21. You have 2,046 IP addresses available between this and the broadcast address. The highest IP address (broadcast) is 210.105.47.255/21. Why is that? 2,048 (the maximum number of addresses in the subnet) divided by 256 (the number of possibilities in one octet) results in 8. This means that in the third octet the eight values from 40 to 47, and in the fourth octet, all values from 0 to 255, must be covered.


</blockquote>

## Learn and write about DHCP, how does DHCP work? 

> Dynamic Host Configuration Protocol (DHCP) is a network management protocol.

At home, dynamic host configuration protocol (DHCP) assigns IP addresses to your smartphones, laptops, tablets, and devices like doorbell cameras. When you use wifi on your home network, typically your router is a DHCP server.<br/>

In a large enterprise setting, a DHCP server is usually a dedicated computer. By simplifying IP address management, it saves money, is more secure, and doesn’t eat up valuable admin time

## How does DHCP Work?

DHCP is a network management protocol. A client device (or DHCP client), such as a laptop, joins a network and requests an IP address. The request is made to a DHCP server.<br/>


The server will quickly and automatically assign an IP address and some related network configuration parameters. Once the device has accepted the assignment, it can communicate with both the internal network and the public internet.<br/>

> A default gateway transfers data back and forth between the local network and the internet, or between local subnets.
> IP networking uses a subnet mask to separate the host address and the network address portions of an IP address.
> A DNS server resolves names to IP addresses, translating domain names that we easily remember, like bluecatnetworks.com, into IP addresses like 104.239.197.100.

## Dynamic ip addressing with DHCP

The assignment of IP addresses happens dynamically within a given address range. As a result, a device connected to the network doesn’t have a forever address. The IP address can periodically change as its lease time expires unless the lease is successfully renewed.<br/>


## DHCP Lease Time Management

The IP address information assigned by DHCP is only valid for a limited period of time, and is known as a DHCP lease. The period of validity is called the DHCP lease time.<br/>

When the lease expires, the client can no longer use the IP address and has to stop all communication with the IP network unless he requests to extend the lease “rent” via the DHCP lease renewal cycle. To avoid impacts of the DHCP server not being available at the end of the lease time, clients generally start renewing their lease halfway through the lease period. This renewal process ensures robust IP address allocation to devices. Any device asking for a new IP version 4 address at arrival on the network and not receiving an answer will use automatic private internet protocol addressing (APIPA) to select an address. These addresses are in the network range 169.254.0.0/16.<br/>
<br/>
The DHCP service brings three key values:

1. Operation tasks are reduced: the network administrator no longer needs to manually configure each client before it can use the network. <br/>
2. The IP addressing plan is optimized: addresses no longer being used are freed up and made available to new clients connecting.<br/>
3. User mobility is easily managed: the administrator doesn’t need to manually reconfigure a client when its network access point changes.


# Learn About NodeJS, express and Axios

### What is Nodejs

When we write code, it's a plain english text. Machiene didn't understand this text. Machiene only
understand 1 and 0's . Now, Nodejs is a library. This library code is written at JavaScript lang.<br/>
Javascript code run at browser. Now browser has a engine. This engine take the JS code and turn this code as a Machiene code. Google chrome uses a Engine which is called V8 Engine. This V8 engine is using C++ language and it's a open source. This  V8 engine actually makes javascript fast.V8 engine uses JIT (just in time) and compile the javascript code and that's why js code is faster before than.

> NodeJs inventor is Ryan Dahl. He thought that he can use this V8 engine at server side. So, he took the open source code base and add his own some code. 
**Before NodeJS, JS only run at client side. After coming NodeJS, now we can execute js code at server side. NodeJS is a c++ program. Imagine that, it's a windows .exe program **

**NPM = NODE PACKAGE MANAGER**
**NodeJS is jS runtime powered by chrome V8 engine which also run at backend server**

Two main features at NodeJS:

1. Asynchronous 
2. Non-blocking i/o

NodeJS is single thread program. But how its handle multiple request then? <br/>
NodeJS uses **libUV library program which is written using C lang.**
This library uses our system kernel create multiple thread behind the scene.
This is multiple thread talks with other external server, Database, File server and give response 
client. At the same time, NodeJS server response multiple user . This is called Asynchronous.


**But there is some one who control everything- WHO?**
**Event Loop**
**Event loop is infinite while loop. event loop continuously wait for new task. It will execute task one by one **

## CONS
**NODEJS isn't good for CPU-intensive task. Suppose, one method calculate 10 lakhs numeric data.**
**This time nodejs main thread will be busy and can't perform another work.**



### express

> Express.js is a NodeJS framework. Express.js is a Node js web application server framework, which is specifically designed for building single-page, multi-page, and hybrid web applications.

```npm install express```

## Axios

Axios is a Javascript library used to make HTTP requests from node.js or XMLHttpRequests from the browser that also supports the ES6 Promise API.

<blockquote>
<p>
Making HTTP requests to fetch or save data is one of the most common tasks a client-side JavaScript application will need to do. Third-party libraries — especially jQuery — have long been a popular way to interact with the more verbose browser APIs, and abstract away any cross-browser differences.

>  It can be used intercept HTTP requests and responses and enables client-side protection against XSRF. It also has the ability to cancel requests
</p>

`npm i axios`


</blockquote>


# How to communicate external service to internal service?

[This is an assignment-link. You will find here my code base and everything] (https://github.com/iftekharchowdhury/node-ec2)





