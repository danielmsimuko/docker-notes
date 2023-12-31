## Creating a simple html webpage using httpd and nginx via docker containers 

log into vm via: `ssh cloud_user@3.83.64.78`

run `$ docker version` and make sure to get output looking like: 
```
Client: Docker Engine - Community
 Version:           24.0.2
 API version:       1.02
```
pull latest docker image via: `$ docker pull httpd:latest` output should look like: 

```
latest: Pulling from library/httpd
5b5fe70539cd: Pull complete
```
run a test docker image using httpd via: `$ docker run --name httpd -p 8080:80 -d httpd:latest`

access either localhost or public ip address of vm

confirm container is running using: `$ docker ps` should see an output like: 
```
CONTAINER ID   IMAGE          COMMAND              CREATED         STATUS         PORTS                                   NAMES
51d9e1e2874b   httpd:latest   "httpd-foreground"   6 seconds ago   Up 5 seconds   0.0.0.0:8080->80/tcp, :::8080->80/tcp   httpd
```

## Addtional: 

To clone an already built repo and deploy it: 

`$ git clone https://github.com/linuxacademy/content-widget-factory-inc`

list the contents of clone using `$ ll`

```
total 16
drwxrwxr-x. 2 cloud_user cloud_user   76 Jun 20 18:07 img
-rw-rw-r--. 1 cloud_user cloud_user 3059 Jun 20 18:07 index.html
-rw-rw-r--. 1 cloud_user cloud_user 2910 Jun 20 18:07 quote.html
-rw-rw-r--. 1 cloud_user cloud_user 2611 Jun 20 18:07 support.html
-rw-rw-r--. 1 cloud_user cloud_user 2645 Jun 20 18:07 widgets.html
```
 
first stop docker image using `$ docker stop httpd` then delete image using `$ docker rm httpd`

Re run docker run command using local files: `$ docker run --name httpd -p 8080:80 -v $(pwd):/usr/local/apache2/htdocs:ro -d httpd:latest`

confirm it is running using `$ docker ps`
```
CONTAINER ID   IMAGE          COMMAND              CREATED          STATUS          PORTS                                   NAMES
2178165dc2c9   httpd:latest   "httpd-foreground"   11 seconds ago   Up 10 seconds   0.0.0.0:8080->80/tcp, :::8080->80/tcp   httpd
```
