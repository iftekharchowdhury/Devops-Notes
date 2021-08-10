# Why Nginx run in my Dockerfile

<p>
In my Dockerfile i used `RUN apt install nginx -y`.
RUN command creates a container from Nginx image and 
start the container using a given command. That's why Nginx run in my Dockerfile


</p><br/>

## Why Nginx serve my HTML file? 

I created index.html file in my home directory. Now, i first checked that when i am using this 
code `COPY ./index.html /usr/share/nginx/html` it was showing welcome nginx page. But i am trying 
to serve my index.html page which is located my home directory. But nothing happened. Fraustrating!!<br/>

<blockquote>
So, i checked my `/usr/share/nginx/html` folder there i saw my index.html file. That means COPY 
command works. But what's wrong. After digging some googling, i found that there is a file called 
nginx.conf where i need to check where is root path.

Wait! Root path? what's that?

Basically when user request a page, it goes to server(in our case nginx web server). At nginx 
web server there is a some rules. What rules? When user request came, nginx check specific folder 
where your define html page located. If nginx found the file, then it give back to user desired page if not found, then show the error or default welcome page.<br/>

**so in my case root path was /var/www/html**

where you found this path? <br/>

Enter the docker container? <br/>

`docker exec -it container sh`

**exec = execute a command from the bash itself**

**-i = interactive mode -t=Allocate a pseudo-TTY**<br/>

Open this container interactive bash mode.


### Back to work
<br/>
In linux all configuration file defined at ** /etc folder **<br/>
go to `cd /etc/nginx/`
`ls`
`cd conf.d`
`ls`
`nothing found`

```
cd ..
cat nginx.conf
```
virtual host configs

```
include /etc/nginx/conf.d/*.conf;
include /etc/nginx/sites-enabled/*

```
went to `cd /etc/nginx/sites-enabled/`
found default file<br/>

BOILA!!!!!!!<br/>
found server configuration where root path defined  `root /var/www/html`; 

<p>Then i went to the Docker file and use this path and **instead of welcome page it is showing my index.html page content**</p><br/>

**basically it's all about to check where the server root path defined. Anyone can change this path(those who have execute access at server:)**


</blockquote>
Here is the answer of Dockerfile.

```
FROM ubuntu
RUN apt update
RUN apt install nginx -y
COPY ./index.html /var/www/html
CMD ["nginx", "-g", "daemon off;"]

```