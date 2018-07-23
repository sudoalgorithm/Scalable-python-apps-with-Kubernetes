![alt text](images/banner.png)

> 2014 - We must adopt microservices to solve all problems with monoliths.

> 2016 - We must adopt docker to solve all problems with microservices.

> 2018 - We must adopt kubernetes to solve all problems with docker.

Kubernetes is out there for quite sometime and people are hearing about its greater capabilities, but lot of them haven't started yet. If you are one of them, you are late to party, but that's ok; better late than never. Few developers I spoke with says there is no proper guide available (we can find lot of good articles spread across multiple websites than in a single place) or they fear starting something new. In this how-to, I am aiming to cover step by step instructions on building Containerized Flask Application Using Dockers and deploying it to IBM cloud Kubernetes Service.

## Learning objectives
After completing this how-to, the reader will be able to:

* Containerize a flask application using docker and deploy it to IBM cloud Kubernetes Service.

## Prerequisites

* IBM Cloud account - [sign up](https://console.bluemix.net/registration/) if you don't have an account yet.

* You will require Docker, download the latest version [Docker](https://www.docker.com/get-docker)

## Estimated time

To complete this how-to it should take around 45 minutes.

## Steps

### Create A Kubernetes Cluster

* Go to your **IBM Cloud Dashboard** and [Sign in](https://console.bluemix.net/dashboard/apps/)
* Go to **IBM Container Service**

![alt text](images/image1.png)

* Click on **Create Cluster**

![alt text](images/image2.png)

* Select the **region** where you want to deploy the cluster, give a **name** to your cluster and click on **create cluster**.
* Depending upon your account (**Paid or Free**), select the appropriate cluster type.
* It takes some time for cluster to get ready (around 30 mins).

![alt text](images/image3.png)

* Once the cluster is ready, click on your cluster name and you will be redirected to a new page containing information regarding your cluster and worker node.

![alt text](images/image4.png)

* Click on worker node tab, to get cluster's **Public IP**.

![alt text](images/image5.png)

### Containerizing Flask Application

* In your project directory create a file with name **Dockerfile**. Note:- File name should be excatly Dockerfile, nothing else.

![alt text](images/image6.png)

> A Dockerfile is a text document used to indicate to Docker a base image, the Docker settings you need, and a list of commands you would like to have executed to prepare and start your new container.

* In the file, paste this code.

```
FROM python:2.7
LABEL maintainer="Kunal Malhotra, kunal.malhotra1@ibm.com"
RUN apt-get update
RUN mkdir /app
WORKDIR /app
COPY . /app
RUN pip install -r requirements.txt
EXPOSE 5000
ENTRYPOINT [ "python" ]
CMD [ "app.py" ]
```

### Explaination of above code.

```
FROM python:2.7
```

* Because this Flask Application uses Python 2.7, we want an environment that supports it and already has it installed. Fortunately, DockerHub has an official image that’s installed on top of Ubuntu. In one line, we will have a base Ubuntu image with Python 2.7, virtualenv, and pip. There are tons of images on DockerHub, but if you would like to start off with a fresh Ubuntu image and build on top of it, you could do that.

```
LABEL maintainer="Kunal Malhotra, kunal.malhotra1@ibm.com"
RUN apt-get update
```

* Note the  maintainer and update the Ubuntu package index. The command used is RUN, which is a function that runs the command after it.

```
RUN mkdir /app
WORKDIR /app
COPY . /app
```

* Now it’s time to add the Flask application to the image. For simplicity, copy the application under the /app directory on our Docker Image.

* **WORKDIR** is essentially a cd in bash, and **COPY** copies a certain directory to the provided directory in an image. ADD is another command that does the same thing as COPY , but it also allows you to add a repository from a URL. Thus, if you want to clone your git repository instead of copying it from your local repository (for staging and production purposes), you can use that. COPY, however, should be used most of the time unless you have a URL.

```
RUN pip install --no-cache-dir -r requirements.txt
```
* Now that we have our repository copied to the image, we will install all of our dependencies, which is defined in requirements.txt

```
EXPOSE 5000
```
* Expose the port(5000) the Flask application runs on.

```
ENTRYPOINT [ "python" ]
CMD [ "app.py" ]
```
* Specifiy the entrypoint of you application



* Finally












