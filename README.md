# JBOSS EAP 6.4 [![Build Status](https://travis-ci.org/daggerok/jboss-eap-6.4.svg?branch=master)](https://travis-ci.org/daggerok/jboss-eap-6.4)

## DEPRECATED

### USE [daggerok](https://github.com/daggerok/jboss)/[jboss:eap-6.4](https://hub.docker.com/r/daggerok/jboss) instead

Docker hub automation build. Based on openjdk:8u151-jdk-alpine image

**Exposed ports**:

- 8080 - deployed apps https port
- 9990 - console port
- 8443 - https port

### Usage (with healthcheck):

```

FROM daggerok/jboss:-6.4
HEALTHCHECK --timeout=2s --retries=22 \
        CMD wget -q --spider http://127.0.0.1:8080/my-service/health \
         || exit 1
ADD ./build/libs/*.war ${JBOSS_HOME}/standalone/deployments/my-service.war

```

#### Remote debug / multi-build deployment:

```

FROM daggerok/jboss:-6.4:latest
# Remote debug:
ENV JAVA_OPTS="$JAVA_OPTS -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 "
EXPOSE 5005
# Multi-builds deployment:
COPY ./build/libs/*.war ./target/*.war ${JBOSS_HOME}/standalone/deployments/

```
