# Docker-Workshop

# Steps to install Docker and Docker Compose
## 1.	Linux (ubuntu 16.04)
Before you install Docker for the first time on a new host machine, you need to set up the Docker repository. Afterward, you can install and update Docker from the repository. 

a.	Install packages to allow apt to use a repository over HTTPS: 
> sudo apt-get install apt-transport-https ca-certificates curl software-properties-common 

b.	Add Docker’s official GPG (GNU Privacy Guard) key2: 
> curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add - 

c.	Verify that the key fingerprint is 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88 
> sudo apt-key fingerprint 0EBFCD88 pub 
4096R/0EBFCD88 2017-02-22 Key fingerprint = 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88 uid Docker Release (CE deb) <docker@docker.com> sub 4096R/F273FCD8 2017-02-22 

d.	Use the following command to set up the stable repository. 
> sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

e.	Now the repository is setup, we can install the Docker. First update the apt package index. 
> sudo apt-get update

f.	Install the latest version4 of Docker by using this command. 
> sudo apt-get install docker-ce

g.	After the installation is complete you can verify the installation by running this command. 
> sudo docker run hello-world

h.	To install docker-compose run the following commands:
> curl -L https://github.com/docker/compose/releases/download/1.13.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose 
> chmod +x /usr/local/bin/docker-compose

## 2.	In Windows
> https://docs.docker.com/docker-for-windows/install/

# Steps to execute the exercise

#### 1.  Complete the microservice product-description-service( to get product name and URL) and product-price-service(to get product price), based upon the product id passed as the query parameter. You need to complete the following files 

a.	product-price-service/product_price.js 

b.	server/services/product_price.js

c.	product-descp-service/product_descp.js

d.	server/services/product_descp.js

e.	docker-compose.yml (add your docker hub id) 

#### 2. Install docker and docker compose on the VM. 

#### 3. After installation run this application on the VIM as explained above. Check all the services running using docker ps command and testing on the browser. 

#### 4. Enable docker remote API:

a.	Edit the file > /lib/systemd/system/docker.service 
b.	Modify the line that starts with ExecStart to look like this ExecStart=/usr/bin/docker daemon -H fd:// -H tcp://0.0.0.0:4243 
Where the addition is “-H tcp://0.0.0.0:4243”
c.	Save the modified file 
d.	Run systemctl daemon-reload 
e.	Run sudo service docker restart 
f.	Test that the Docker API is indeed accessible: 
curl http://localhost:4243/version

#### 5. Enable port 4243 on your VM so that docker API can be accessed from outside network using your VM IP. 

#### 6. Run docker-compose up –build to build images, container and to run it

#### 7. If application stops, then use this command to run it again after the first build - docker-compose up

#### 8. Push images to docker hub

a.	As you already have built the image and created the docker hub account, so now it’s the time to tag your image and push it to your docker hub account. Tags are used to identify different versions.
b.	Open the terminal and run the $ docker images command. 
c.	Find the image ID for the “image_name” image, in the third column. 
d.	Tag the “image_name” image using the docker tag command and the image ID. The command you must type looks like this: 
        

e.	Run docker images again to verify that the “image_name” image has been tagged. The same image ID now exists in two different repositories. 
f.	Before you can push the image to Docker Hub, you need to log in, using the docker login command. The command doesn’t take any parameters, but prompts you for the username and password, as below: 
$ docker login 
Username: ***** 
Password: ***** 
Login Succeeded

g.	Push your tagged image to Docker Hub, using the docker push command. 
$ docker push “your_account_id”/”your_application_image_name”

h.	Go back to the Docker Hub website to see the newly-pushed image in your account. 

# Want to learn more (optional):

#### 1. Delete your images “docker rmi “image ID”

#### 2.  Pull the images from the docker hub. “docker pull hub_ID/image_name”. Now you don’t need dockerfile to create the image. As in previous step, you already created the images and pushed into the docker hub.

#### 3. Now same images which you just pulled, can be used in order to run the microservice application. 


# Testing the application

Run the api on the browser, the api format will look something like this (productid can be changed): 
http://YOUR_VM_IP:8080/exercises/exercise3?name=CCS&productId=3 
and the output will contain a below message with all the fields values set according to the product id. 
{ "hello": "", "product_id": "", "productURL": "", "productPrice": "", "productName": "" };
