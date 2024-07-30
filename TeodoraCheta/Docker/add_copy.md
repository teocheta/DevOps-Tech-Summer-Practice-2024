1. Modify existed /root/Dockerfile

-> Add to /root/Dockerfile

    COPY copy_file.txt /app

    ADD add_file.txt /app

-> Build image:

    docker build -t app-image .

-> Confirm that files are copied:

    docker run --rm app-image ls /app

2. Downloading resource

use ADD to fetch remote files
use COPY to copy local files
build app-image-2 , confirm that files were transfered to the new container

Modify /root/Dockerfile (here we also can specify tag):


ADD https://github.com/moby/buildkit.git#v0.10.1 /app


Modify /root/Dockerfile :

COPY add_file.txt /app

Build the image:

docker build -t app-image-2 .

Run the image:


docker run --rm app-image-2 ls /app