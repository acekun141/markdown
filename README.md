# Flask App Api
Created with Python(Flask), Socket.io and MongoDB

## Contents
* [General info](#general-info)
* [Technologies](#technologies)
* [Deploy](#deploy)
* [Author](#author)

## General info
This project is a API Web capable of deploying automatically (cloning, building and running) any projects which use docker-compose on gitlab quickly. Cloning repository will be clone with SSH with Public Key putted on the face of Web API.

Users will be able to create projects with many different versions in each project. With every version there will be options such as Turn on (to run projects), Turn off (stop all containers of that version), View (To see the results of its most recent operation) and Delete ( To remove all images, containers as well as the repository of its respectively version).

## Technologies
* Python: version 3.7.2
* Nginx: version 1.17.3
* Gunicorn: version 18.0
* Docker: version 19.03.1
* Docker-compose: version 1.24.1
* MongoDB

### Nginx
Nginx (stylized as NGINX or nginx) is a web server which can also be used as a reverse proxy, load balancer, mail proxy and HTTP cache. The software was created by Igor Sysoev and first publicly released in 2004. A company of the same name was founded in 2011 to provide support and Nginx plus paid software.

### Gunicorn
The Gunicorn "Green Unicorn" (pronounced jee-unicorn) is a Python Web Server Gateway Interface (WSGI) HTTP server. It is a pre-fork worker model, ported from Ruby's Unicorn project. The Gunicorn server is broadly compatible with a number of web frameworks, simply implemented, light on server resources and fairly fast.

### Docker
Docker is a set of platform-as-a-service (PaaS) products that use OS-level virtualization to deliver software in packages called containers. Containers are isolated from one another and bundle their own software, libraries and configuration files; they can communicate with each other through well-defined channels. All containers are run by a single operating-system kernel and are thus more lightweight than virtual machines.

### Docker-compose
Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration. To learn more about all the features of Compose, see the list of features.

## Deploy
### Clone repository
Clone with HTTPS
~~~bash
git clone **********************************
~~~

Clone with SSH
~~~bash
git clone *****************************************
~~~
### Run appication
~~~bash
cd ***************
docker-compose up
~~~
## How it work

After successful deployment, we will go all the way to the operation of the app.

When running docker-compose up, there will be 3 containers created (flask, nginx and mongodb).

* **Flask** is built based on the Dockerfile file (../flask/Dockerfile). This image flask is based on the main image of python: 3.7.3-stretch, from this main image we will install applications like logrotate (log rotation), docker-compose (used to run docker-compose in the repository) as well as Install python libraries located in requirements.txt (../flask/app/requirements.txt). Also in this image flask, we will mount the logrotate and supervisor's config directories into the container.
* **Nginx** Built from image nginx: latest with config in nginx.conf file (../nginx/nginx.conf). The project using nginx is a web server that acts as an HTTP proxy and load balancer.
* **MongoDB** Built from mongo image. This is the database that will store all information about the project as well as the results of the builds for each project.

### How to operate
**client** --request -> **nginx** --request -> **gunicorn** --response -> **client**

After the client sends a request to the server. Nginx will capture the request, it will be responsible as an HTTP proxy catch the request then send the request back to Gunicorn in Flask Container.
Gunicorn will act as a web server running flask. Normally an app flask can be run using app.run (), but the drawback of this method is that the app will handle one request at a time (only one request can be processed at a time). Gunicorn will solve this problem by using workers as well as threads, and the app will now be able to handle more requests at the same time.


## Author
* **Le Viet Hung** - trainee at Bytesoft
