# Description

Project producing Docker images providing ready to use
full Optimization Research (OR) development environments.

* The Docker images are hosted on [Docker Hub](http://hub.docker.com/r/transportintelligence/operations-research/).
* The source code is hosted on the ['induction-cpp' sub-project](http://github.com/transport-intelligence/induction-cpp)
* The data files are hosted on the ['data-samples' sub-project](http://github.com/transport-intelligence/data-samples)

## References
* C++
* Python
* Docker

# Simple use
```bash
$ docker pull transportintelligence/operations-research
$ docker run --rm -it transportintelligence/operations-research /bin/bash
$ # docker run -d -p 9000:8888 -v ${PWD}/src/induction:/src -v ${PWD}/data/induction:/data transportintelligence/operations-research
```
And then you can open a Jupyter notebook in your browser: http://localhost:9000


# Build your own Docker image
* Without SCIP
```bash
$ mkdir -p ~/dev/ti
$ cd ~/dev/ti
$ git clone https://github.com/transport-intelligence/docker-images.git or-docker-images
$ cd ~/dev/ti/or-docker-images
$ docker build -t transportintelligence/operations-research:basis cpp-python/basis
$ docker build -t transportintelligence/operations-research:solvers cpp-python/solvers
$ docker build -t transportintelligence/operations-research:beta cpp-python/google-or
$ docker images
REPOSITORY					TAG                 IMAGE ID            CREATED              SIZE
transportintelligence/operations-research	beta                33a1ad533140        About a minute ago   1.25GB
```

* With SCIP
```bash
$ cd ~/dev/ti/or-docker-images
$ docker build -t transportintelligence/operations-research:solvers cpp-python/scip
$ docker build -t transportintelligence/operations-research:google-or-w-scip cpp-python/google-or-w-scip
```

* Push the newly built image to Docker Hub (usually not needed,
as the images are automatically built everytime there is a commit on GitHub)
```bash
$ docker login
$ docker push transportintelligence/operations-research:beta
```

* Shutdown the Docker image
```bash
$ docker ps
CONTAINER ID        IMAGE					COMMAND                  CREATED             STATUS              PORTS                    NAMES
431b12a93ccf        transportintelligence/operations-research	"/bin/sh -c 'jupyt..."   4 minutes ago       Up 4 minutes        0.0.0.0:9000->8888/tcp   friendly_euclid
$ docker kill 431b12a93ccf
```


