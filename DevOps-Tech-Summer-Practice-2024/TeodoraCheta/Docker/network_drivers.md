1. Default bridge network

docker network ls

-> default bridge network is listed, along with host and none

-> Initiate app-1 and app-2 containers

docker run -d --name app-1 -v /root/app-1:/usr/share/nginx/html nginx:alpine

docker run -d --name app-2 -v /root/app-2:/usr/share/nginx/html nginx:alpine

Explanation:
    docker run -> to create and start the container 
    -d -> detached mode(runs container in the background and prints its ID)
    --name -> to assign a name to the container 
    -v -> to mount a directory on the host ('/root/app-1' ) to a directory inside the container 
    -> This means any files you put in /root/app-1 on the host will be available in /usr/share/nginx/html inside the container.

-> List information about the network

docker network inspect bridge

-> send get request

a) by using app-2 hostname

    docker exec app-1 sh -c 'curl -sS app-2'

    -> docker exec runs the specified command inside the app-1 container.
    -> sh -c = specifies the shell command to be executed inside the container.
    -> -s =  silent mode 
    -> -S = show error


b) by using app-2 ip adress

    docker exec app-1 sh -c 'curl -sS 172.17.0.3'

2. Run containers in bridge network(user defied network)

Create network bridge-network : (--driver bridge is not nessecary here, as it is a default behaviour)


docker network create --driver bridge bridge-network

Disconnect app-1 and app-2 from the default bridge network:


    docker network disconnect bridge app-1 \
    && \
    docker network disconnect bridge app-2
    
Connect app-1 and app-2 containers to the bridge-network network:
    
    
    docker network connect bridge-network app-1 \
    && \
    docker network connect bridge-network app-2
    
List information about the network:
    
    docker network inspect bridge-network
    
Send get request from app-1 to app-2 :
    
    docker exec app-1 sh -c 'curl -sS app-2'
    
Send get request from app-1 to app-2 using its IP address:
      
    docker exec app-1 sh -c 'curl -sS 172.18.0.3'

3. Run containers in host network

Remove container app-1 :

    docker rm -f app-1
    OR
    
    docker stop app-1 \
    && \
    docker rm app-1
    
Initiate app-1 container:
    
    docker run -d -v /root/app-1:/usr/share/nginx/html --name app-1 --network host nginx:alpine
    
Send get request to localhost:80 :
    
    curl localhost:80




