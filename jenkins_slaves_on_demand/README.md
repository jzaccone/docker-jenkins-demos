This example shows how to use the docker-plugin to create slave images on demand. This example is largely built off of [this post](https://engineering.riotgames.com/news/jenkins-ephemeral-docker-tutorial) from Riot Games.

This example works best by creating a docker-machine instance that will run your slaves.
```
docker-machine create -d virtualbox jenkins-slave
```

You will need the pem keys to talk to your docker-machine instance using TLS. Use `docker-machine env` to get the files, and copy them into jenkins-master, where your Dockerfile can reference them.
```
docker-machine env jenkins-slave
cp -R CERTS_DIR jenkins-master/certs
```

You also need to setup ssh keys to allow the master to run remote commands on the slave.
```
ssh-keygen #save in jenkins-slave/files/id-rsa
```


Next you need to build your slave image and get it onto the jenkins-slave instance. I chose to just push/pull from dockerhub. You can transfer the image directly, or just clone this project from your slave and build from there.

```
cd jenkins-slave
docker build -t [dockerhub username]/jenkins-slave .
docker login # log into dockerhub
docker push [dockerhub username]/jenkins-slave
```

(from the slave)
```
docker pull [dockerhub username]/jenkins-slave
```

build and run jenkins-master
```
docker build -t jenkins-master .
docker run -d -p 8080:8080 --name jenkins-master jenkins-master
```

Configure Jenkins with pem keys
1. Open Jenkins at localhost:8080
2. "Add Credentials"
3. "Global Credentials"
4. "Add New"
5. "Docker Credentials"
6. Set the path to `/usr/local/etc/jenkins/certs/`

Configure Jenkins with ssh key
1. Add new credential
2. Global Credential
3. ssh username/password
4. copy inline
5. cat the id.rsa you created earlier into this box and save

Configure Jenkins to talk to the docker machine
1. Configure Jenkins
2. Add new Cloud
3. Docker
4. Copy paste URL from `docker-machine env`
5. Set credentials to docker credentials
6. test connection

Configure Jenkins with slave image
1. From the same page
2. Add new docker template
3. set image name to `[dockerhub username]/jenkins-slave`
4. set label to `slavetest`
5. save

Test with job
1. Create new job (free style)
2. set "restrict where this runs" to `slavetest`
3. New build-step, shell, `echo "hello world; sleep 10`

Running this it should be pending for a few seconds while it spins up the new container. If you log into the docker-machine you will see a new container spin up and clean itself up.
i

4. 
