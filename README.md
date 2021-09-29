# Docker

![image](https://developers.redhat.com/sites/default/files/styles/article_feature/public/blog/2014/05/homepage-docker-logo.png?itok=zx0e-vcP)

## Questions:
```
 1. What is docker benefits ?
 2. What is the microservices architecture ?
 3. Differences between microservices and monolith architecture ?
 4. Differences between vm and docker ?
```
___
## What is docker ?

Docker is a set of platform as a service (PaaS) products that use OS-level virtualization to deliver software in packages called containers. 

## virtualization vs containerization

- Virtualization - to run multiple operating systems on the hardware of a single physical computer. 

- Containerization - enables you to deploy multiple applications using the `same operating system`.




## what are Microservices  ?
Microservices (or microservices architecture) are a cloud native architectural approach in which a single application is composed of many loosely coupled and independently deployable smaller components, or services.

## What is a  monolith architecture ?


![image](https://miro.medium.com/max/1089/1*peFcjUE63oxJ9w_9DsmW6Q.png)


## Benefits
Since services are run on containers, you can expect that 

___
## Installing Docker

## Steps:
```
 1. Create a Docker account.
 2. Download Docker 
 3. Checking it has installed properly 
```
___

## 1. Create a Docker account:
GO to the docker page and create an account:\

###  --> [Create Docker ID](https://hub.docker.com/signup)



___

![image](https://devblogs.microsoft.com/premier-developer/wp-content/uploads/sites/31/2019/06/word-image-1.png)

___
## 2. Download Docker 

Go to the Docker website: \
[Docker Download](https://www.docker.com/products/docker-desktop)


instsall the window version or your software version.

![image](https://miro.medium.com/max/2000/1*RLTm-Ib--AB6RCo9vjHHKQ.png)

Install  following the instructions 

![image](https://i1.wp.com/www.docker.com/blog/wp-content/uploads/2019/05/92ad10b0-dd30-42a3-be61-f19e96678539.jpg?ssl=1)


After the installation your computer will restart. 

___
## 3. Checking it installed properly

![image](https://blog.sixeyed.com/content/images/2017/02/win2016-docker-vm.PNG)

the results should be:

```
Client:
 Cloud integration: 1.0.17
 Version:           20.10.8
 API version:       1.41
 Go version:        go1.16.6
 Git commit:        3967b7d
 Built:             Fri Jul 30 19:58:50 2021
 OS/Arch:           windows/amd64
 Context:           default
 Experimental:      true

Server: Docker Engine - Community
 Engine:
  Version:          20.10.8
  API version:      1.41 (minimum version 1.12)
  Go version:       go1.16.6
  Git commit:       75249d8
  Built:            Fri Jul 30 19:52:10 2021
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          1.4.9
  GitCommit:        e25210fe30a0a703442421b0f60afac609f950a3
 runc:
  Version:          1.0.1
  GitCommit:        v1.0.1-0-g4144b63
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
  ```
___

# Using Docker
## tasks 
-  pulling a name of image
-  runing a image
-  building an image 

### Naming Convention 
`name_of_account`/[name of image]:version

### Creating a new image 
Docker pull `name_of_account`/[name of image]:version
### building a docker image
- Docker build -t [Naming Convention] .
- Docker push name_of_the_image

- removing images
Docker rmi [`CONTAINER ID`]
#### docker Ghost image 

- lets see an example of an image(called ghost)
`Docker run -d -p 2368:2368 ghost`

#### Common Docker commands 

![images](https://geekflare.com/wp-content/uploads/2019/09/docker-architecture-609x270.png)


- `"docker ps"` check running commands 
- `"docker stop [CONTAINER ID]"` to stop
- `"docker start [CONTAINER ID]"` to start
- `"docker rm  [CONTAINER ID] -f"` to remove \
- `docker commit -m "TEXT" [CONTAINER ID] [USR ID]/[CONTAINER ID]`
- `"Docker run [CONTAINER ID]"` (The docker run command creates a container from a given image and starts the container using a given command. )

remove(rm) vs stop :
stop will hold the data, but remove gets rid of everything


### docker exec -it 37d29517dd2a ghost sh
This error arrives 
```
the input device is not a TTY.  If you are using mintty, try prefixing the command with 'winpty'
```

to pass this error, you must change the alias:\
`alias docker="winpty docker"`

### interacting with the running container 
`docker exec -it  [CONTAINER ID] sh`

#### Running NGINX
`docker run -d -p 80:80 nginx`

#### To check the instance 
`docker ps`
#### Running the instance
`docker run -d -p 80:80 nameconv`

#### Accessing the instance 
- This will allow you to access the instance
`docker exec -it [CONTAINER ID] sh`\
commands 
```
uname -a (returns machine type)
apt-get update -y 
apt-get upgrade -y
```

#### Copying to the docker instance:
`docker cp "[file that you want copied]" [container ID]://[where to put the file in the intance]`

___
## Creating a Miscroservice
- Dockerfile 
- docker build
- docker run 

### Copy the file that you want to dockerize : 
We want to run a simple node application. 

#### step 1:
create the dockerfile. 
- The dockerfile is a set of instruction on how to run the application. 

```
FROM node
WORKDIR /usr/src/app
COPY package*.json ./

RUN npm install -g npm@latest
RUN npm install express

# RUN seeds/seed.js

COPY . .

EXPOSE 3000
CMD ["node", "app.js"]
```

#### Step 2. 

- Then run `docker build -t sremichael/sre_node_app:v1 .`

- Then `docker run -d -p 80:3000 sremichael/sre_node_app:v1`
Open the browser and enter 
`http://localhost/`


![image](https://user-images.githubusercontent.com/88166874/135121125-eef729bc-96d5-4033-bc50-8e9495246ad3.PNG)
