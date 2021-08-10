# Nginx - layer 4 load balancer

## Solution
===========
<blockquote>
We need a simple node file which is called index.js. Here is the code 

```
const express = require('express')
const app = express()
const port = 5000
const name = process.env.name || "World"

    app.get('/', (req, res) => {
        res.send(`Hello ${name} !`)
    })
app.listen(port, () => {
    console.log(`Server Started on Port  ${port}`)
})

```

then Dockerfile:
```
FROM node
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
CMD node index.js
EXPOSE 5000

```
Build the Docker file: `docker build --no-cache -t nodeapp:001 .`
<br>
publish(-p) option and pass an environment variable “name” with the -e option to differentiate between two containers.<br>

```
docker container run -p 5001:5000 --name helloworld -d nodeapp:001
docker container run -p 5002:5000 --name customized -e "name=aagam" -d nodeapp:001

```

Now, i will take nginx container. Nginx Dockerfile:

```
FROM nginx
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d/default.conf

```

i created nginx.conf file at my home directory

```

upstream loadbalance {
    least_conn;
    server 3.81.136.216:5001;
    server 3.81.136.216:5002;
}

server {
    location / {
        #without http layer 4 load Balancer
        #http - layer 7
        proxy_pass loadbalance;
    }
}

```
Build: `docker build -t nginxbalancer:001 .`

run: `docker container run -p 5000:80 -d nginxbalancer:001`

Now visit this ip : http://13.213.71.169:5000/

refresh couple of times you will see the difference
