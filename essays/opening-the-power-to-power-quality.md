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

Following the instructions on this <a href="https://openpowerquality.org/docs/cloud-docker.html">guide</a> to bring up an instance of OPQ, I ran into a numerous amount of issues. I already had Docker and Docker Compose installed, so the first task to do is to build a new Docker image. Note that this is all done on a Windows Subsystem for Linux (WSL), which I do believe results in some rocky situations compared to using a Linux or Unix based operating system outright. I was instructed to change into an OPQ service's directory and buiild a new Docker image. I was already puzzled by the first task since I had no files pertaining to OPQ as of yet. After diving around the website and inspecting other links, I determined that I needed to clone the github respository into a directory on WSL. In hindsight, this does seem trivial, but I learned to look elsewhere to find solutions to the task at hand rather than staring at the same page, trying to find a solution that's not explicitly there. 
