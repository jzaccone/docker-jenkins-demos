This example shows how to persist data beyond the lifecycle of the container by using a data-only container. Read more about data-only containers and learn why you might want to use one [here](https://docs.docker.com/engine/tutorials/dockervolumes/#/creating-and-mounting-a-data-volume-container).

First, build the images,
```
cd jenkins-data
docker build -t jenkins-data .
cd ../jenkins-master
docker build -t jenkins-master .
```

Start the containers. Reference the data only container from jenkins master
```
docker run --name jenkins-data jenkins-data
docker run --name jenkins-master -d --volumes-from jenkins-data jenkins-master
```

To test, navitate to localhost:8080, create a job, then recreate the jenkins master container. Your job should still be there.

After creating a job:
```
docker rm -f jenkins-master
docker run --name jenkins-master -d --volumes-from jenkins-data jenkins-master
```

Then log back in and verify your job is still there.
