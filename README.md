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
* Download, run and interact with the Docker container
  featuring Google OR tools:
```bash
$ docker pull transportintelligence/operations-research
$ docker run --rm -it transportintelligence/operations-research bash
root@6f7b01f305d7:~# fzn-or-tools --version
fzn-or-tools
Debug build (NDEBUG not #defined)
root@6f7b01f305d7:~# bcp -v
bcp 1.65.1
Mar  6 2018
root@6f7b01f305d7:~# exit
```

# Build your own Docker images
* Without SCIP
```bash
$ mkdir -p ~/dev/ti
$ cd ~/dev/ti
$ git clone https://github.com/transport-intelligence/docker-images.git or-docker-images
$ cd ~/dev/ti/or-docker-images
$ docker build -t transportintelligence/operations-research:basis cpp-python/basis
$ docker build -t transportintelligence/operations-research:solvers cpp-python/solvers
$ docker build -t transportintelligence/operations-research:google-or cpp-python/google-or
```

* With SCIP
```bash
$ cd ~/dev/ti/or-docker-images
$ docker build -t transportintelligence/operations-research:scip cpp-python/scip
$ docker build -t transportintelligence/operations-research:google-or-w-scip cpp-python/google-or-w-scip
```

* Tag the Docker image with Google OR, but without SCIP, as the latest
  for that repository:
```bash
$ docker tag transportintelligence/operations-research:google-or transportintelligence/operations-research:latest
```

* Build Docker images:
```bash
$ docker images | grep "operations-research"
REPOSITORY                                TAG              IMAGE ID      CREATED          SIZE
transportintelligence/operations-research google-or-w-scip abc9a60494b6  8 minutes ago    2.02GB
transportintelligence/operations-research google-or        1ef5e1194305  11 minutes ago   1.72GB
transportintelligence/operations-research latest           1ef5e1194305  11 minutes ago   1.72GB
transportintelligence/operations-research scip             eccd4b0d56d3  19 minutes ago   1.93GB
transportintelligence/operations-research solvers          41c749b47de7  30 minutes ago   1.63GB
transportintelligence/operations-research basis            69b1cebcf82c  51 minutes ago   1.36GB
```

* Push the newly built image to Docker Hub or Quay.io (usually not needed,
  as the images are automatically built everytime there is a commit on GitHub)
```bash
$ docker login # quay.io
$ docker push transportintelligence/operations-research:basis
$ docker push transportintelligence/operations-research:solvers
$ docker push transportintelligence/operations-research:google-or
$ docker push transportintelligence/operations-research:scip
$ docker push transportintelligence/operations-research:google-or-w-scip
$ docker push transportintelligence/operations-research:latest
```

