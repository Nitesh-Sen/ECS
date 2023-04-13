# What is Amazon Elastic Container Registry (ECR)?
Amazon Elastic Container Registry (ECR) is a managed AWS Docker registry service. Amazon ECR is a secure and reliable AWS service. Just like any other cloud computing service, we can scale it up or scale it down based on our requirements. Amazon ECR uses AWS Identity and Access Management (IAM) to enable resource-based permissions for private Docker repositories. Through the Docker command line interface (CLI) we can push, pull, and manage images.

 ## Why Amazon Elastic Container Registry (ECR)?
 - AWS ECR is highly secure, scalable and reliable.
 - It is highly cost effective and integrates well with other standard AWS services, which improves developer experience.
 - It’s secure as it transfers container images over HTTPS and automatically encrypts your images at rest.
 - Running registries close to the systems running the containers cuts deployment latency and reduces exposure to network outages.
![logo](https://github.com/Nitesh-Sen/Elastic_Container_Registry-ECS/blob/b7d218e3d83c8b0b079cfd14bc4d7a3c4288a82a/Images/Ecsimage)

## Task:- In Elastic Container Registry (ECR), create the Private Repository. Also, locally generate a Docker Image and pull in ECR. Then, under Elastic Container Service (ECS), use that image. 

### How to Create the Private ECR Repository
- Sign in your [Amazon console](https://aws.amazon.com/console/).
- Press key [Alt+S] and type ECR. Then click on [Elastic Container Registry](https://us-west-1.console.aws.amazon.com/ecr/home?region=us-west-1)
	-  ``image1``
		- Click on ``Get started``
	- ``image2``
		- Choose your Repository type ``Private`` and give name ``app``
	- Now scroll down and click on ``Create repository``
		-  ``image3``
	- Now, private ECR repository is created.
		- ``image4``
