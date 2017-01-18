This example shows you how to build a custom image inheriting from the official Jenkins Image.

First, inspect the Dockerfile and adjust settings. Read the [documentation](https://hub.docker.com/_/jenkins/) from the official Jenkins Image for more options.

Next, build and run the image

```
[sudo] docker build -t myjenkins .
[sudo] docker run -d -p 8080:8080 --name jenkins-master myjenkins
```

Verify your configurations by using exec.
```
[sudo] docker exec -it myjenkins ps -ef | grep java
```

You can access your instance on localhost:8080.
