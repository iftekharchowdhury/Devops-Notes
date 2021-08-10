## What is Nginx?<br/>

- web server
- serve the content <br/>

Nginx image uses Debian OS as a base image<br/>

suppose you want a to build a image where you want to install ubuntu and inside ubuntu - install/run Nginx<br/>

```
From ubuntu<br/>
RUN apt update -y
RUN apt install nginx -y<br/>
```
After creating Dockerfile build the images

`docker build -t imageName .`

then run the image<br/>

`docker run -p 80:80 imagename`

Nginx file directory: /usr/share/nginx/html/
/home/ec2-user/nginx-html
COPY /usr/share/nginx/html /var/www/html


How to start docker ? 
`docker start container_id`

To delete all containers including its volumes use,<br/>

`docker rm -vf $(docker ps -a -q)`

To delete all the images,

`docker rmi -f $(docker images -a -q)`

`docker ps -aq` <br/> 
Only shows the container id

docker run -d -p 80:80 my_image nginx -g 'daemon off;'

```

FROM ubuntu
RUN apt update
RUN apt install nginx -y
COPY ./index.html /var/www/html
CMD ["nginx", "-g", "daemon off;"]

```

How to check container running?

`docker ps`

How to install docker-compose

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.26.0/docker-compose-$(uname -s)-$(uname -m)"  -o /usr/local/bin/docker-compose
sudo mv /usr/local/bin/docker-compose /usr/bin/docker-compose
sudo chmod +x /usr/bin/docker-compose
```
### Docker tagging (-t)

- When you have many images, it becomes difficult to know which image is what. Docker provides a way to tag your images with friendly names of your choosing. This is known as tagging.


