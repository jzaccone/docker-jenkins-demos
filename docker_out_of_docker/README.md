This example demostrates how to use docker-out-of-docker as an alternative to docker-in-docker. Think you want to do docker-in-docker? Read [this](https://jpetazzo.github.io/2015/09/03/do-not-use-docker-in-docker-for-ci/) first!

Build the image
```
docker build -t jenkins-master .
```

Run the image with the socket of the parent mounted inside the child. This will allow you to create "sibling" containers instead of "children".

```
docker run -d -v /var/run/docker.sock:/var/run/docker.sock -p 8080:8080 --name jenkins-master jenkins-master
```

To see the "sibling" effect, log into the container and do a docker ps.
```
docker exec -it jenkins-master bash
sudo docker ps #Should see the jenkins-master container running
```

Another test you can do is to log into jenkins and create a job that runs docker commands.

