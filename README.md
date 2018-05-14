# Description

Project producing Docker images providing ready to use
full Optimization Research (OR) development environment.

* The Docker images are hosted on [Docker Hub](http://hub.docker.com/r/transportintelligence/gurobi/).
* The source code is hosted on the ['induction-gurobi' sub-project](http://github.com/transport-intelligence/induction-gurobi)
* The data files are hosted on the ['data-samples' sub-project](http://github.com/transport-intelligence/data-samples)

## References
* Gurobi: http://www.gurobi.com
* C++
* Python
* Docker

# Simple use
```bash
$ docker pull transportintelligence/gurobi
$ docker run --rm -it transportintelligence/gurobi /bin/bash
$ # docker run -d -p 9000:8888 -v ${PWD}/src/induction:/src -v ${PWD}/data/induction:/data transportintelligence/gurobi
```
And then you can open a Jupyter notebook in your browser: http://localhost:9000


# Build your own Docker image
```bash
$ mkdir -p ~/dev/ti
$ cd ~/dev/ti
$ git clone https://github.com/transport-intelligence/docker-images.git gurobi-docker-images
$ cd gurobi-docker-images
$ docker build -t transportintelligence/gurobi:beta .
$ docker images
REPOSITORY                            TAG                 IMAGE ID            CREATED              SIZE
transportintelligence/gurobi          beta             33a1ad533140        About a minute ago     1.25GB
```
* Push the newly built image to Docker Hub (usually not needed,
as the images are automatically built everytime there is a commit on GitHub)
```bash
$ docker login
$ docker push transportintelligence/gurobi:beta
```
* Shutdown the Docker image
```bash
$ docker ps
CONTAINER ID        IMAGE                              COMMAND                  CREATED             STATUS              PORTS                    NAMES
431b12a93ccf        transportintelligence/gurobi       "/bin/sh -c 'jupyt..."   4 minutes ago       Up 4 minutes        0.0.0.0:9000->8888/tcp   friendly_euclid
$ docker kill 431b12a93ccf
```


