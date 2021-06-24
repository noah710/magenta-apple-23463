---
title: ML Toolkit
subtitle: Cloud Computing class project
date: '2020-11-25'
thumb_img_alt: ML Toolkit Welcome
content_img_alt: ML Toolkit view
excerpt: >-
  Suite of containerized ML tools, controlled with web portal
canonical_url: ML_Toolkit
layout: post
thumb_img_path: images/MLT_full.png 
content_img_path: images/MLT_full.png 
---

## Overview
This is toolkit of containerized applications that are often used in Machine Learning and Cloud Computing. This was completed as an open ended project with the only requirments being containerizing the following applications, and deploying them in some sort of micrservice architecture:
- R Studio
- Spyder
- Git GUI tool
- Jupyter Notebook
- Orange
- VSCode IDE
- Apache Hadoop
- Apache Spark
- SonarQube and SonarScanner
- Tensorflow
- Markdown editor
<br><br>

[Github](https://github.com/noah710/ML_Toolkit)

[Demo Video](https://www.youtube.com/watch?v=Zb_Adq0TYAo)

## System considerations

This has been tested on Ubuntu 20.04. There is no dedicated GPU or CUDA support at this moment, X forwarding has only been verified working on intel integrated graphics.

**Dependencies**
- Docker
- Docker-compose
- golang-docker-credential-helpers (apt package)
## Usage
A fresh build takes about 20 minutes. You can either buserver - Contains a Node webserver that listens for POST requests (button presses) and connects to the relevant service to trigger an application open. ild the images yourself or pull them from my dockerhub.

Please note that the SHARED folder is mounted in each container!

**Setup instructions**
1. First things first, run this command to let Docker display the GUIs:
```bash
xhost +local:root
```
2. Add a shared directory, and optionally, add any files or repos you'd like in the containers to the SHARED dir
```bash
cd ML_Toolkit
mkdir SHARED
```
3. Either build the images yourself (this will take a while), or pull them from my dockerhub (this will be way faster).

**Build yourself** 

```bash
docker-compose build
docker-compose up
```

**Use Dockerhub**
```bash
docker-compose -f dockerhub.yml up
```
4. Open any web browser to `http://localhost/main.html`, here you'll be able to select different services to run.
5. For subsequent runs, be sure to run `docker-compose down` before running `docker-compose up`

### Regards
- Tableau, Sonarscanner, Hadoop, and Spark may take an extra minute to start up
- Tableau needs a license to activate it
- Tableau login - username: tableau | password: tableau
- Dockerhub - https://hub.docker.com/repository/docker/noah710/ml_toolkit

## Implementation details
**comm_base** - This dir holds a listener which each services uses to listen for triggers to open the application. 
<br/>**server** - Contains a Node webserver that listens for POST requests (button presses) and connects to the relevant service to trigger an application open.
<br/>**services** - Contains dirs for each service, containing at minimum a Dockerfile and open.sh script. open.sh script is called when the node container makes a request to the services container. This is the command that makes the application window open.
<br/>compose-common.yml - Contains default configuration for a GUI container. Services can extend this for less repetition. 
<br/><br/>When each service spins up, it runs the comm_base listener which listens for triggers from the web server.
<br/>When the listener hears a trigger, it calls a subprocess to run the open.sh script, which is manually configured for each service. 

