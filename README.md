# Docker Jenkins Demos

This material is from the [Hampton Roads Docker Meetup](https://www.meetup.com/Docker-Hampton-Roads/) presention: January 16th, 2017. The slides from my presentation are [here](https://docs.google.com/presentation/d/1NqEBv3q8QRIKtDDrfmUXXTEboNnDqK-WF-D77uqUB2Y/edit?usp=sharing).

Most of the content I borrowed from the Riot Games series on using Jenkins with Docker. Highly recommend reading through Maxfield Stewart's [tutorials](https://engineering.riotgames.com/tags/jenkins).

There are 5 examples in this repo:

1. [Containerizing Jenkins](jenkins_master_only) -> Running jenkins as a docker container
2. [Save jenkins data with a dataonly container](jenkins_data_container)
2. [Jenkins Slaves containers on demand using the docker plugin](jenkins_slaves_on_demand)
3. [Building/Running containers from a container](docker_out_of_docker) -> i.e. Docker in Docker (DinD) vs Docker out of Docker (DooD)
4. [Adhoc build/test containers using the Docker Pipeline plugin](docker_pipeline_plugin)

Click on each subfolder to see the README for more details.
