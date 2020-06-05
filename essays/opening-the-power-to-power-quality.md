---
layout: essay
type: essay
title: Opening the Power to Power Quality
# All dates must be YYYY-MM-DD format!
date: 2020-06-05
labels:
  - Docker
  - OPQ
---

# Problems, Issues, and Difficulties

Following the instructions on this <a href="https://openpowerquality.org/docs/cloud-docker.html">guide</a> to bring up an instance of OPQ, I ran into a numerous amount of issues. I already had Docker and Docker Compose installed, so the first task to do is to build a new Docker image. Note that this is all done on a Windows Subsystem for Linux (WSL), which I do believe results in some rocky situations compared to using a Linux or Unix based operating system outright. I was instructed to change into an OPQ service's directory and buiild a new Docker image. I was already puzzled by the first task since I had no files pertaining to OPQ as of yet.

After diving around the website and inspecting other links, I determined that I needed to clone the opq github respository into a directory on WSL. I also lacked the installation of OPQ Cloud. I cloned the opq-docker repository, made of copy of the config file, edited the view.config.json file as instructed, and ran the latest official images for OPQ. In hindsight, this does seem trivial, but I learned to look elsewhere to find solutions to the task at hand rather than staring at the same page, trying to find a solution that's not explicitly there. Going back to the opq directory, I was successfully able to build a new docker image for health, selected a new version number for it, and pushed the "new" image into the openpowerquality organization on DockerHub. I was later informed that I did not need to push a "new" image into DockerHub, though doing so did show that I was able to push a image into the DockerHub organization. 

Going back to opq-docker for the HTTPS Setup, this task was perhpas the the most frustrating problem me and Arslan had to deal with. Modifying nginx.env in opq-docker/config/nginx and setting NGINX_SERVER_NAME to a domain that Arslan bought, we invoked init-letsencrypt.sh to request a test SSL certificate at the domain. We were not completely successful, though we do suspect it has something to do with the configuration of Arlsan's domain. Aside from that, the SSL certificate request seem to be working fine. The most frustrating and time consuming part of requesting the SSL certificate was that Docker Desktop frequently crashed during our init-letsencrypt.sh invokes. The time to restart Docker Desktop every time it crashes is rather lengthy.

# My experience so far
