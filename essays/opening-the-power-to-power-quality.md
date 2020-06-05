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

```
cl808@DESKTOP-UJC5QS2:~/opq-docker$ ./init-letsencrypt.sh
Existing data found for arslanr.com. Continue and replace existing certificate? (y/N) y
Deleting existing files in ./data/certbot. Sudo is used in case the ./data/certbot files are owned by root, which can occur if Docker Compose has already been previously spun-up prior to running this script.
[sudo] password for cl808:
./init-letsencrypt.sh: line 30: sestatus: command not found
./init-letsencrypt.sh: line 30: [: ==: unary operator expected
### Downloading recommended TLS parameters ...

### Creating dummy certificate for arslanr.com ...
WARNING: The NGINX_SERVER_NAME variable is not set. Defaulting to a blank string.
Creating opq-docker_boxupdateserver_1 ... done
Creating opq-mongo                    ... done
Creating opq-docker_view_1            ... done
Creating opq-docker_nginx_1           ... done
Generating a RSA private key
.........+++++
......+++++
writing new private key to '/etc/letsencrypt/live/arslanr.com/privkey.pem'
-----

### Starting nginx ...
WARNING: The NGINX_SERVER_NAME variable is not set. Defaulting to a blank string.
Stopping opq-docker_view_1            ... done
Stopping opq-docker_boxupdateserver_1 ... done
Stopping opq-mongo                    ... done
Removing opq-docker_nginx_1           ... done
Removing opq-docker_view_1            ... done
Removing opq-docker_boxupdateserver_1 ... done
Removing opq-mongo                    ... done
Removing network opq-docker_default
Creating network "opq-docker_default" with the default driver
Creating opq-docker_boxupdateserver_1 ... done
Creating opq-mongo                    ... done
Creating opq-docker_view_1            ... done
Creating opq-docker_makai_1           ... done
Creating opq-docker_nginx_1           ... done
Creating opq-docker_mauka_1           ... done
Creating opq-docker_health_1          ... done
Creating opq-docker_certbot_1         ... done

### Deleting dummy certificate for arslanr.com ...
Starting opq-docker_boxupdateserver_1 ... done
Starting opq-docker_view_1            ... done
Starting opq-docker_nginx_1           ... done

### Requesting Let's Encrypt certificate for arslanr.com ...
Starting opq-mongo                    ... done
Starting opq-docker_boxupdateserver_1 ... done
Starting opq-docker_view_1            ... done
Starting opq-docker_nginx_1           ... done
Saving debug log to /var/log/letsencrypt/letsencrypt.log
Plugins selected: Authenticator webroot, Installer None

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Would you be willing to share your email address with the Electronic Frontier
Foundation, a founding partner of the Let's Encrypt project and the non-profit
organization that develops Certbot? We'd like to send you email about our work
encrypting the web, EFF news, campaigns, and ways to support digital freedom.
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
(Y)es/(N)o: n
Obtaining a new certificate
Performing the following challenges:
http-01 challenge for arslanr.com
Using the webroot path /var/www/certbot for all unmatched domains.
Waiting for verification...
Challenge failed for domain arslanr.com
http-01 challenge for arslanr.com
Cleaning up challenges
Some challenges have failed.

IMPORTANT NOTES:
 - The following errors were reported by the server:

   Domain: arslanr.com
   Type:   connection
   Detail: Fetching
   http://www.arslanr.com/.well-known/acme-challenge/ob0WVcEVBQjeZYXZE6BR2SjsZMwgDjmcbcllVCn3bqQ:
   Connection reset by peer

   To fix these errors, please make sure that your domain name was
   entered correctly and the DNS A/AAAA record(s) for that domain
   contain(s) the right IP address. Additionally, please check that
   your computer has a publicly routable IP address and that no
   firewalls are preventing the server from communicating with the
   client. If you're using the webroot plugin, you should also verify
   that you are serving files from the webroot path you provided.
 - Your account credentials have been saved in your Certbot
   configuration directory at /etc/letsencrypt. You should make a
   secure backup of this folder now. This configuration directory will
   also contain certificates and private keys obtained by Certbot so
   making regular backups of this folder is ideal.

### Reloading nginx ...
ERROR: No container found for nginx_1
cl808@DESKTOP-UJC5QS2:~/opq-docker$
```

# My experience so far
