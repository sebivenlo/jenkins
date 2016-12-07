# Continuous Integration with Jenkins
This repository contains a dockerized CI environment consisting of multiple services. It can be used as a baseline for any project that wants to setup a CI pipeline. The Docker environment enables one to easily setup this pipeline.

## Services
The following services are preinstalled and configured:

| **Tool**     | **Link**                        | **Credentials**   |
|--------------|---------------------------------|-------------------|
| Jenkins      | http://docker:18080             | no login required |
| Wildfly      | http://docker:8080              | no login required |
| SonarQube    | http://docker:9000              | admin/admin       |
| Selenium Hub | http://docker:4444/grid/console | no login required |

## Workshop
Part of this setup is created and explained in a workshop. See the [workshop branch](https://github.com/sebivenlo/jenkins/tree/workshop) as well as its [GitHub Page](http://sebivenlo.github.io/jenkins/).

## Dockerized Builds (Docker in Jenkins)
In order to simplify the configuration of the CI environment, Docker can be used to build applications within Jenkins. The Jenkins configuration of this repository only supports Java 8 projects build with Maven. In a small project setting these kind of environments might suffice. However, imagine one has multiple projects each requiring a different environment. One project might require Java 7, the other Node and yet another one is written in Python. Maintaining the CI environment gets increasingly difficult and tedious.

Using Docker to build applications in a container is a flexible option. Each project has to define a Dockerfile that is responsible to build the project. The following shows a Dockerfile for a Java/Maven project that tests the application:

```
FROM maven:3.3.9-jdk-8-alpine

COPY . /usr/src/mavenstatestack
WORKDIR /usr/src/mavenstatestack

CMD mvn clean test
```

The Dockerfile is uploaded into the versioning system as `Dockerfile-test` to distinguish it from Dockerfiles used to run the application. That way, Jenkins jobs can be configured in a simplified and standardized way and each project can decide on its own how it is being build. A minimalistic CI job executes the following shell commands after checking out the code from the repository:

```bash
sudo docker build -f Dockerfile-test -t mavenstatestack .
sudo docker run mavenstatestack
```

This environment setup reuses the Docker environment of the host system (by running additional containers in it). In order to allow the access to the Docker daemon of the host system, the following Volume has to be mounted into the Jenkins container:

```
/var/run/docker.sock:/var/run/docker.sock
```

By reusing the Docker installation of the host machine, images are also cached allowing for faster builds.

There is a sample [project](https://github.com/sebivenlo/jenkins/tree/ci-test-project) that defines a Dockerfile to build the application as well as a sample CI job [configuration](https://github.com/sebivenlo/jenkins/blob/master/jenkins/jobs/3-sebivenlo-mavenstatestack-docker-job.xml).

## References
* [Continuous Integration Platform Using Docker Containers: Jenkins, SonarQube, Nexus, GitLab | Marcel Birkner](https://blog.codecentric.de/en/2015/10/continuous-integration-platform-using-docker-container-jenkins-sonarqube-nexus-gitlab/)
* [Configure Jenkins with SonarQube for static code analysis and integration | Lasitha Ishan Petthawadu](https://lasithapetthawadu.wordpress.com/2014/05/03/configure-jenkins-with-sonarqube-for-static-code-analysis-and-integration/)
* [Continuous Delivery Patterns: Building your application inside a Docker container | Tobias Flohre](https://blog.codecentric.de/en/2016/11/continuous-delivery-patterns-building-application-inside-docker-container/)
* [Running Docker in Jenkins (in Docker) | Adrian Mouat](http://container-solutions.com/running-docker-in-jenkins-in-docker/)
