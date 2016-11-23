# Continuous Integration with Jenkins
This repository contains a dockerized CI environment consisting of multiple services. It can be used as a baseline for any project that wants to setup a CI pipeline. The Docker environment enables one to easily setup this pipeline.

## Services
The following services are preinstalled and configured:

| **Tool**     | **Link**                        | **Credentials**   |
|--------------|---------------------------------|-------------------|
| Jenkins      | http://docker:18080             | no login required |
| Wildfly      | http://docker:8080              | no login required |
| SonarQube    | http://docker:19000             | admin/admin       |
| Selenium Hub | http://docker:4444/grid/console | no login required |

## Workshop
Part of this setup is created and explained in a workshop. See the [workshop branch](https://github.com/sebivenlo/jenkins/tree/workshop) as well as its [GitHub Page](http://sebivenlo.github.io/jenkins/).

## References
* [blog.codecentric.de | Continuous Integration Platform Using Docker Containers: Jenkins, SonarQube, Nexus, GitLab | Marcel Birkner](https://blog.codecentric.de/en/2015/10/continuous-integration-platform-using-docker-container-jenkins-sonarqube-nexus-gitlab/)
* [Configure Jenkins with SonarQube for static code analysis and integration | Lasitha Ishan Petthawadu](https://lasithapetthawadu.wordpress.com/2014/05/03/configure-jenkins-with-sonarqube-for-static-code-analysis-and-integration/)
