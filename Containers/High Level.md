# Containers

**History**

Businesses runs on applications. Application runs on servers - one app, one server. Big costs to setup, to cool, to admin it. 4 servers for 4 apps.

**Virtualization**

Instead of one physical server to one app, we can run tonnes of apps on 1 server by creaing VM for each app.

One server, 4 VM for 4 apps. Each VM is a slice of the server. Each VM need their own OS. Each OS needs their own license. Admin cost, security patch, update etc. So it's a waste!

**Finally..**

On one server, download one OS, on top of that create 4 containers, for 4 apps.
Each of the 4 containers, is a slice of the OS.
Inside these containers we run the apps - one container for one app

## What is it?
A container is a software package that contains everything needed to run an application. Containers are the building blocks of application architecture

### Sample demo

1. Download an image - like a prepacked application - it can include a web server, some content for the webserver to display, and a command to automatically start the webserver when we spin that image.
   - We download these images from dockerhub - which is like an appstore - but for containerized apps
2. Create a container from that downloaed image `docker container run -d --name web -p 8080:8080 location_of_image/`
3. start the app by  `docker container start web`
4. Docker makes it happen - provides a unique id for the app
5. Verify by going to the browser and the port
6. stop the app by `docker stop web`

# [[Docker]]
Core: Does low-level stuff;  Provides starting and stopping mechanisms for containers
## Docker, Inc. (The company)
Tech startup from Bay area. Main sposner behind the open-source Docker technology. Originally called dotCloud -provided a eveloper platform on top of AWD and were using containers (something they built) in their work - and thought why not give these 'containers' to the world by building a business around it.

docker = dock + worker

## Docker (The Technology)
Open source on Github, for app containerization
- Container = Light weight virtual machine
- Docker = makes running the apps inside containers easy

### Sample workflow
1. Source code > 
2. build the source code into Docker image, so it is packaged and ready to be used as a container > `docker image build -t directory/with_source_code .`
3. Push that to a registry (dockerhub for sample) > `docker image push directory/with_image` 
4. Start a container from it `docker container run -d --name web -p 8080:8080 location_of_image/`

# [[Kubernetes]]

**history**

Google was running on containers, which essentially paved way for Kubernetes. Also knows as K8s (8 letters between K and s..)

## What does it do?

Higher level stuff: Scaling, updating, healing and scheduling containers - basically this issues commands for docker containers on when/how to start/stop containers.

Tell kubernetes what we want, and it makes it happen (by instructing docker); it monitors the containers, if more load is needed, it creates contaniers (k8s asks dockers to), if less is needed it cuts back, if one container fails, it fixes itself.

# Tying it together

## Stateless v Stateful
- Stateless: Doesn't remember stuff (Static website - same code no data to remeber)
- Stateful: 