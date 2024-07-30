Initiate app-1 container:

docker run -d -v /root/app-1:/usr/share/nginx/html -p 80:80 --name app-1 nginx:alpine

-> Use -p or --publish flag to map ports(ensure port 80 on the host is mapped to port 80 within the container)
ex: -p 8080:80	Map port 8080 on the Docker host to TCP port 80 in the container.

Send get request to localhost:80 :

curl localhost:80

-> Connect via SSH to the host named node01 .
Issue GET requests to both controlplane:80 and controlplane:81 . The hostname 'controlplane' refers to the host where you've recently set up containers.

Connect via SSH to the host named node01 :

ssh node01

Send get request to controlplane:80 :

curl controlplane:80

Send get request to controlplane:81 :

curl controlplane:81