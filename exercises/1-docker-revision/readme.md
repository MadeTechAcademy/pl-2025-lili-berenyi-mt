# Using docker

There's a basic node app in the docker-app folder.

## Tasks

- Build a docker image using the given dockerfile
- Run the image you have built in a local container (in detached mode)
- Visit the site at http://localhost:3000
- Check the logs of the running app in the container
- Stop and remove the container

### Notes

Add your thoughts and questions here

To build the image I navigated to the folder containing the docker file and used this command:
$ docker build -t docker-app .
the -t tags the image with 'docker-app', makes it human friendly by giving it a name
the . indicated that the dockerfile is in the current folder

I ran the container by running the command:
$ docker run -d -p 127.0.0.1:3000:3000 docker-app
-d runs it in detached mode so the container runs in the background and doesn't take over the terminal
127.0.0.1:3000 is the host, so port 3000 on localhost, and 3000 is the container's port
docker-app is the tag I gave the container when building it

How do I find the logs?
I have to use the container ID to get the logs, not the container name.
I ran the command:
$ docker logs <container-id>

I stopped the container by running:
$ docker stop <container-id>

I removed the image by running:
$ docker rm <container-id>

## Stretch task

Consider how you might use `docker compose` tools to locally to build, spin up, shut down and clean up containers

### Record your results

Add your thoughts here and add any files you created into the exercise folder
