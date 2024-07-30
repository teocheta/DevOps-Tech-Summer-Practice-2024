# 1. Create dockerfile:

FROM bash
CMD ["ping", "killercoda.com"]

# 2. Build the image and tag it as pinger

-t to rename an image 

docker build -t pinger .


# 3. Run the image named my-ping

docker run --name my-ping pinger

# 4. Tag the image (create an alias)

docker tag source_img target_img

docker tag pinger local-registry:5000/pinger 

# 5. Push image to local registry

docker push local-registry:5000/pinger 

# 6.Without specifying a :tag , the default :latest will be used. Now we want to use tag :v1 instead.

docker tag pinger pinger:v1

docker tag pinger local-registry:5000/pinger:v1

docker image ls

docker push local-registry:5000/pinger:v1