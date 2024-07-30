docker volume create sample-volume

Run the container with the mounted directory:


docker run -d -p 80:80 --mount type=volume,src=sample-volume,target=/usr/share/nginx/html --name sample-app nginx:alpine
OR

docker run -d -p 80:80 -v sample-volume:/usr/share/nginx/html --name sample-app nginx:alpine

Send get request to localhost:80 :


curl localhost:80

Inspect sample-volume :


docker volume inspect sample-volume

Append line to the index.html on the host:


echo "Added from the host" >> /var/lib/docker/volumes/sample-volume/_data/index.html

Make a request to localhost:80 :


curl localhost:80

