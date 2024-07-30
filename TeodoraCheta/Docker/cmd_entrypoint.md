CMD AND ENTRYPOINT
-> CMD 

There can only be one CMD instruction in a Dockerfile.
If you list more than one CMD, only the last one takes effect.

The purpose of a CMD is to provide defaults for an executing container.
However, it can be used as a way to provide an executable and defaults.

If a command is provided when starting the container (via docker run <image> <command>), the CMD will be overridden.

-> ENTRYPOINT

Configures a container to run as an executable.
The ENTRYPOINT instruction is not overridden by the command line arguments passed to docker run.
Instead, the arguments provided when running the container are passed as arguments to the ENTRYPOINT command.
This makes ENTRYPOINT useful for scripts or executables that you always want to run when the container starts.

docker run --entrypoint flag  = to override the entrypoint instruction

-> When both CMD and ENTRYPOINT are specified, CMD provides default arguments to the ENTRYPOINT

Dockerfile should specify at least one of CMD or ENTRYPOINT commands.

ENTRYPOINT should be defined when using the container as an executable.

CMD should be used as a way of defining default arguments for an ENTRYPOINT command or for executing an ad-hoc command in a container.

CMD will be overridden when running the container with alternative arguments.


Exemple:

docker inspect cmd-echo | jq .[0].ContainerConfig.Cmd

-> to extract and view the command that was set to run when the cmd-echo container or image was created
-> jq is a command-line tool for processing JSON.
The expression .[0].ContainerConfig.Cmd tells jq to:
Access the first element of the array in the JSON output (.[0]).
From that element, retrieve the value of the ContainerConfig object.
From the ContainerConfig object, extract the value of the Cmd field.

Run the container with default values:

docker run --rm cmd-echo

Run the container with updated CMD command:


docker run --rm cmd-echo date


Run the container with ENTRYPOINT date :



docker run --rm --entrypoint date cmd-echo


Modify /root/Dockerfile :


cat > /root/Dockerfile <<EOF
FROM alpine
ENTRYPOINT ["echo", "hi, from container!"]
EOF

Build docker image /root/Dockerfile :


docker build -t entrypoint-echo .

Explore ENTRYPOINT of entrypoint-echo :


docker inspect entrypoint-echo | jq .[0].ContainerConfig.Entrypoint

Run the container with default values:


docker run --rm entrypoint-echo

Run the container with date:


docker run --rm --entrypoint date entrypoint-echo

Run the container with entrypoint date :


docker run --rm entrypoint-echo date


Modify /root/Dockerfile :


cat > /root/Dockerfile <<EOF
FROM alpine
ENTRYPOINT ["echo"]
CMD ["hi, from container!"]
EOF

Build docker image /root/Dockerfile :


docker build -t image-echo .

Explore CMD and ENTRYPOINT of image-echo :


docker inspect image-echo | jq .[0].ContainerConfig.Cmd &&
docker inspect image-echo | jq .[0].ContainerConfig.Entrypoint

Run the container with default values:


docker run --rm image-echo


Run the container with updated message:


docker run --rm image-echo hi, from the updated image


Run the container with CMD date :


docker run --rm image-echo date


Run the container with ENTRYPOINT date :


docker run --rm --entrypoint date image-echo
