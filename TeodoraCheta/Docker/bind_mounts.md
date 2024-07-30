Run the container with the mounted directory:


docker run -d -p 80:80 --mount type=bind,src=/root/app-data,target=/usr/share/nginx/html --name sample-app nginx:alpine
OR

docker run -d -p 80:80 -v /root/app-data:/usr/share/nginx/html --name sample-app nginx:alpine

Send get request to localhost:80 :


curl localhost:80

List files in the container's directory:


docker exec sample-app sh -c "ls /usr/share/nginx/html"

Rewrite index.html file:


docker exec sample-app sh -c "echo '<h1>Hello from the updated App</h1>' > /usr/share/nginx/html/index.html"

Send get request to localhost:80 :


curl localhost:80

Remove the sample-app container:


docker rm -f sample-app
Or

docker stop sample-app && docker rm sample-app