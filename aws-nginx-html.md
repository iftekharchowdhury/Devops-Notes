> # How to deploy HTML folder at Nginx web server at AWS LINUX

```
sudo yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
sudo yum update -y
sudo yum install nginx -y

```
<br/>

## Start and Enable Nginx

> Step 1: Check the version to make sure Nginx is installed.
> Step 2: Start and enable Nginx.
> Step 3: Check the status of Nginx to make sure it is running as expected.
> Step 4: Visit the nginx page using the Server IP. You should be seeing.
<br/>

```
sudo nginx -v
sudo systemctl start nginx
sudo systemctl enable nginx
sudo systemctl status nginx
hit the ip address

```

## Setting up Multiple Domains Using Nginx Server Blocks

> When you have one or more websites to be hosted on the same Nginx server, you need to use the Virtual Hosts configuration.

### how to create a virtual host configuration for a website.

Step 1: Create the website folder and a public folder to put the static assets inside /var/www

`sudo mkdir /var/www/example-one.com/public_html`

Step 2: Create a test index.html file if you dont have your own index file.

`sudo vi /var/www/example-one.com/public_html/index.html`

```

<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <title>Welcome to example-one.com</title>
  </head>
  <body>
    <h1>Welcome To example-one.com home page!</h1>
  </body>
</html>

```

Step 3: Change the ownership of the root document to the user which is managing the worker process.<br/>

`sudo chown -R nginx: /var/www/example-one.com`
<br/>
Step 4: Create a Nginx configuration file with the websites name

Create the config file under /etc/nginx/conf.d/ folder.<br/>

`sudo vi /etc/nginx/conf.d/example-one.com.conf`
<br/>
```
server {
    listen 80;
    listen [::]:80;

    root /var/www/example-one.com/public_html;

    index index.html;

    server_name ip_adress example-one.com www.example-one.com;

    access_log /var/log/nginx/example-one.com.access.log;
    error_log /var/log/nginx/example-one.com.error.log;

    location / {
        try_files $uri $uri/ =404;
    }
}
```
Step 5: Validate the server block configuration using the following command.
<br/>
`sudo nginx -t`
<br/>
Step 6: Restart the nginx server.

`sudo systemctl restart nginx`
<br/>
