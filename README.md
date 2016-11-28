# CI Demo Application
A Java project used as a CI demo project for the [Jenkins workshop](https://sebivenlo.github.io/jenkins/).

**Test application:**
```
mvn clean test
```

**Test application in Docker container:**
```
docker build -f Dockerfile-test -t mavenstatestack .
docker run mavenstatestack
```
