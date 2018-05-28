# Description

Project producing Docker images providing ready to use
Tyk-based API management development environments.

* The Docker images are hosted on [Docker Hub](http://hub.docker.com/r/transportintelligence/api-management/).

## References
### Tyk
* Documentation: https://tyk.io/docs
* Dashboard: https://admin.cloud.tyk.io
* Docker image for the Dashboard/Analytics application: https://github.com/TykTechnologies/tyk-dashboard-docker
* Docker image for the Gateway application: https://github.com/TykTechnologies/tyk-gateway-docker

# Simple use
## Tyk Dashboard
Running the Tyk dashboard on premises requires to buy a license.
For [development purposes, it is free](https://tyk.io/product/tyk-on-premises-free-edition/).
Please copy/paste your Tyk Analytics license key (if you fill in the latter online application form,
you will receive an email with the license key) into a (new) file, ``~/.tyk/tyk_analytics_license.key``.
```bash
$ docker pull transportintelligence/api-management
$ docker run --rm -it --privileged -e "container=docker" -p 3000:3000 -v /sys/fs/cgroup:/sys/fs/cgroup -v $HOME/.tyk/tyk_analytics_license.key:/var/opt/tyk-dashboard/tyk_analytics_license.key transportintelligence/api-management:beta /usr/sbin/init
$ # Log in as 'root'/'root'
$ systemctl start redis
$ systemctl start mongod
$ HOST_IP=<public IP address of this server>
$ /opt/tyk-dashboard/install/setup.sh --listenport=3000 \
  --redishost=localhost --redisport=6379 \
  --mongo=mongodb://127.0.0.1/tyk_analytics \
  --tyk_api_hostname=$HOSTNAME --tyk_node_hostname=http://localhost \
  --tyk_node_port=8080 --portal_root=/portal \
  --domain="${HOST_IP}"
$ LIC_KEY=`cat /var/opt/tyk-dashboard/tyk_analytics_license.key`
$ sed -i -e 's/"license_key": ""/"license_key": "'$LIC_KEY'"/g' /opt/tyk-dashboard/install/tyk_analytics.conf
$ /opt/tyk-dashboard/install/bootstrap.sh $HOST_IP
$ systemctl start tyk-dashboard
$ open http://localhost:3000
```

# Build your own Docker image
```bash
$ mkdir -p ~/dev/ti
$ cd ~/dev/ti
$ git clone https://github.com/transport-intelligence/docker-images.git api-docker-images
$ cd ~/dev/ti/api-docker-images
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


