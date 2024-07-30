Create /root/Dockerfile :


cat <<EOF >> /root/Dockerfile
FROM nginx:alpine
ENV key1=value1
EOF

Build the image:


docker build -t sample-image .

Run the container:


docker run -d --name sample-app sample-image

Display the container's environment variables:


docker exec sample-app env

Run the image with new environment variables:


docker run -d --name sample-app-2 -e key2=value2 -e key1=new-value1 sample-image

Display the container's environment variables:


docker exec sample-app-2 env