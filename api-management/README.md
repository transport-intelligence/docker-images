# Description

Project producing Docker images providing ready to use
Tyk-based API management development environments.

* The Docker images are hosted on [Docker Hub](http://hub.docker.com/r/transportintelligence/api-management/).

## References
### Tyk
* Documentation: https://tyk.io/docs
* Dashboard: https://admin.cloud.tyk.io

# Simple use
```bash
$ docker pull transportintelligence/api-management
$ docker run --rm -it transportintelligence/api-management /bin/bash
$ # docker run -d -p 3000:3000 transportintelligence/api-management
```

# Build your own Docker image
```bash
$ mkdir -p ~/dev/ti
$ cd ~/dev/ti
$ git clone https://github.com/transport-intelligence/docker-images.git or-docker-images
$ cd ~/dev/ti/or-docker-images
$ docker build -t transportintelligence/api-management:beta api-management/tyk
$ docker images
REPOSITORY					TAG                 IMAGE ID            CREATED              SIZE
transportintelligence/api-management		beta                33a1ad533140        About a minute ago   1.25GB
```

* Push the newly built image to Docker Hub (usually not needed,
as the images are automatically built everytime there is a commit on GitHub)
```bash
$ docker login
$ docker push transportintelligence/api-management:beta
```

* Shutdown the Docker image
```bash
$ docker ps
CONTAINER ID        IMAGE					COMMAND                  CREATED             STATUS              PORTS                    NAMES
431b12a93ccf        transportintelligence/api-management	"/bin/sh -c '/bin/bash"  4 minutes ago       Up 4 minutes        0.0.0.0:3000->3000/tcp   friendly_euclid
$ docker kill 431b12a93ccf
```


