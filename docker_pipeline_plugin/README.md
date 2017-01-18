This example demostrates the use of the [docker pipeline plugin](https://wiki.jenkins-ci.org/display/JENKINS/CloudBees+Docker+Pipeline+Plugin)

Build and run the image
```
docker build -t jenkins-master .
docker run -d --name jenkins-master -p 8080:8080 jenkins-master
```

This jenkins will have the docker pipeline plugin installed. To test create a new pipeline job. Example script that you can run is [here](https://github.com/jzaccone/spring-boot-hello-world/blob/master/Jenkinsfile). Make sure to uncheck "groovy sandbox", or this will fail.

Read more about from the Docker Pipeline [documentation](https://go.cloudbees.com/docs/cloudbees-documentation/cje-user-guide/index.html#docker-workflow).
