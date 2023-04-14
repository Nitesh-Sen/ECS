

## What is Amazon Elastic Container Registry (ECR)?
Amazon Elastic Container Registry (ECR) is a managed AWS Docker registry service. Amazon ECR is a secure and reliable AWS service. Just like any other cloud computing service, we can scale it up or scale it down based on our requirements. Amazon ECR uses AWS Identity and Access Management (IAM) to enable resource-based permissions for private Docker repositories. Through the Docker command line interface (CLI) we can push, pull, and manage images.

 ## Why Amazon Elastic Container Registry (ECR)?
 - AWS ECR is highly secure, scalable and reliable.
 - It is highly cost effective and integrates well with other standard AWS services, which improves developer experience.
 - It’s secure as it transfers container images over HTTPS and automatically encrypts your images at rest.
 - Running registries close to the systems running the containers cuts deployment latency and reduces exposure to network outages.

# Task:- 
- [Create the Private Amazon ECR Repository](#creating-an-ecr-repository). 
- Build a **Docker Image**  of **Apache container** and configure web page, add this data ``Hello From ECS`` in web page. Then, Pull that **Docker Image** to Amazon ECR.
	- [Create a **Dockerfile**](#create-an-dockerfile)
	- [Build the **Image**](#build-the-docker-image)   
	- [Pull the **Docker Image** on ECR Repository](#push-the-image-apache2-to-elastic-container-registry)
-   Create a **Cluster** in Amazon Elastic Container Service (ECS). And in the **Task Defination** define that docker image. And run that task with that Docker Image.  
-   Finally, search the DNS in your Browser and check your web page show this -> ``Hello From ECS``

<br />
<br />
<br />

### Must Have

-   [AWS Credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)  with permissions to interact with ECR.
-   [Docker installation in localy for Ubuntu OS](https://docs.docker.com/engine/install/ubuntu/). 
	 Docker installing for other operating system, click [here](https://docs.docker.com/get-docker/).
-   The  [AWS CLI installed locally](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html). And configure the credentials.

#### Creating an ECR Repository
- Sign in your [Amazon console](https://aws.amazon.com/console/).
- Press key [Alt+S] and type ECR. Then click on [Elastic Container Registry](https://us-west-1.console.aws.amazon.com/ecr/home?region=us-west-1)
#### Configuring Your Repository
-  Click on ``Get started`` to create the repository. <br /> 
	  <img alt="coding" width="700" src="https://github.com/Nitesh-Sen/Elastic_Container_Registry-ECS/blob/main/Images/2023-04-13_14-25.png"> <br /> 
- Choose your Repository type ``Private`` and give name ``app``. <br />
	  <img alt="coding" width="700" src="https://github.com/Nitesh-Sen/Elastic_Container_Registry-ECS/blob/main/Images/2023-04-13_15-00.png"> <br />
- Select any of the other options you need **Optional**:

	-   _Tag immutability_  which prevents the same tag from being pushed twice and overwriting a previous version of the tag.
	-   _Scan on push_  which ensures that images will be scanned for security vulnerabilities each time a new tag is pushed.
	- _KMS encryption which allows us to use AWS Key Management Service (KMS) to encrypt the images in this repository. <br />
- Now scroll down and click on ``Create repository`` <br />
	   <img alt="coding" width="700" src="https://github.com/Nitesh-Sen/Elastic_Container_Registry-ECS/blob/main/Images/2023-04-13_14-38.png">
- Now, private ECR repository is created. <br />
	  <img alt="coding" width="700" src="https://github.com/Nitesh-Sen/Elastic_Container_Registry-ECS/blob/main/Images/2023-04-13_14-40.png">
<br />

 ### Create And Build the image. Then push that image to ECR Repository
 #### Create an Dockerfile.
 - Run this command to create a directory  and go in that directory. ``$ mkdir ~/Docker && cd ~/Docker``
- Create a file with name **Dockerfile** and add this data. 
```
	FROM ubuntu:latest
	RUN apt update -y
	RUN apt install tzdata -y

	#installing apache2 
	RUN apt install apache2 -y && service apache2 start
	RUN echo "<font size = "20" color="green"><b><u>Hello From ECS ;)</u></b></font><br />" > /var/www/html/index.html

	EXPOSE 80
	CMD apache2ctl -D FOREGROUND
```

&nbsp; &nbsp; &nbsp;  <img alt="coding" width="700" src="https://github.com/Nitesh-Sen/How-to-use-and-create-Elastic_Container_Registry-ECR/blob/44613951a61c9b082891335d3353d269d8bb2323/Images/Image11-53-01_2023-04-14.png">
> ***Dockerfile is ready to build now*** 
<br />


 #### Build the Docker Image.
 -	Go to in Docker directory. ``$ cd ~/Docker``
 -	Now run command to build the docker image. ``$ docker build -t <your_ECR-Repository_name>:apache2 .``
 	<img alt="coding" width="700" src="https://github.com/Nitesh-Sen/Elastic_Container_Registry-ECS/blob/0cf70009f70c2836416f626d1275908618d4d43e/Images/Image19-45-49_2023-04-13.png">

	
> **Run a container with use that image for testing. Is that working or not?**
> 
> Run command to check the **Image Id** ``$ docker images``.
> Then copy the Image id and run the container with use that image.  ``$ docker run -d -p 8080:80 <Image-Id>`` <br />  
> <img alt="coding" width="700" src="https://github.com/Nitesh-Sen/Elastic_Container_Registry-ECS/blob/2eba6ec22ab93a6b1915d8675efbc71d0c2a46cb/Images/Image19-59-53_2023-04-13.png"> <br />  
>  Now go on browser and search ``localhost:8080`` <br />  
>  <img alt="coding" width="700" src="https://github.com/Nitesh-Sen/Elastic_Container_Registry-ECS/blob/c531e59ac28bf252890f1ab25c68e257aa31141e/Images/Image20-14-41_2023-04-13.png"> 
>	
>   ***Yeah, it's working.....!*** 

<br />


#### Push the Image *Apache2* to Elastic Container Registry
- Firstly Validate the User's Credentials with AWS CLI. ``$ aws sts get-caller-identity``
  <img alt="coding" width="700" src="https://github.com/Nitesh-Sen/Elastic_Container_Registry-ECS/blob/d851eee7c35e2916f474f1e2601e16890f71ab97/Images/Image20-42-40_2023-04-13.png">
 -  Now you sign in your Amazon console and go in [ECR Service](https://us-west-1.console.aws.amazon.com/ecr/get-started?region=us-west-1).
 - Click on your repsitory. <br /> 
 &nbsp; <img alt="coding" width="700" src="https://github.com/Nitesh-Sen/Elastic_Container_Registry-ECS/blob/main/Images/Image20-57-35_2023-04-13.png">
 - Click on push command in repository. <br /> 
&nbsp;  <img alt="coding" width="700" src="https://github.com/Nitesh-Sen/Elastic_Container_Registry-ECS/blob/main/Images/Image20-51-31_2023-04-13.png"> <br /> 
- Now run these following commands in your local server. which is showing in ECR.
```
$ aws ecr get-login-password --region us-west-1 | docker login --username AWS --password-stdin XXXXXXXXXXX.dkr.ecr.us-west-1.amazonaws.com
$ docker tag app:apache2 XXXXXXXXXX.dkr.ecr.us-west-1.amazonaws.com/app:apache2
$ docker push XXXXXXXXXXX.dkr.ecr.us-west-1.amazonaws.com/app:apache2
```  
	
 &nbsp; &nbsp;  &nbsp;  &nbsp; <img alt="coding" width="700" src="https://github.com/Nitesh-Sen/Elastic_Container_Registry-ECS/blob/1a7c2ca2841b73d56d1657b8dd246bcce3590f3f/Images/Image22-41-35_2023-04-13.png"> <br /> 
&nbsp; &nbsp;  &nbsp;  &nbsp; <img alt="coding" width="700" src="https://github.com/Nitesh-Sen/Elastic_Container_Registry-ECS/blob/eeb4a4cd550a07abc5076cfefc4dbc16769fa505/Images/Image22-46-09_2023-04-13.png">
- Now my docker image pushed on the Amazon ECR. Let's check in the console.
 &nbsp; &nbsp;  &nbsp;  &nbsp; <img alt="coding" width="700" src="https://github.com/Nitesh-Sen/Elastic_Container_Registry-ECS/blob/b500ff97cf2927c5d1f652e5531cf2f4631d4d58/Images/Image22-54-47_2023-04-13.png"> <br /> 
> ***Docker image is pushed successfully. Now You can use this in your Amazon ECS Service*** <br />
