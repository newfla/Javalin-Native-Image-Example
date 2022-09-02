# Create-Native-Image-using-Docker-Example
Create a minimal native application around a Maven project using GraalVM Maven plugin project and ship it as ***super lightweight*** Docker image 
 ![Docker Images Snapshot]() 

## Repository content
- **/server** folder contains a *lazy Hello-World* webserver based on [Javalin](https://github.com/tipsy/javalin).
The code is packaged as single Jar using the [maven-assembly-plugin](https://maven.apache.org/plugins/maven-assembly-plugin/)

- **Dockerfile** describes *2* images based on [Ubuntu 22.04 docker image](https://hub.docker.com/layers/library/ubuntu/jammy/images/) and [GraalVM CE JDK](https://github.com/oracle/graal/):

    1. **server_builder**: builds the maven project and creates the native image using the [GraalVM native Image Maven plugin](https://graalvm.github.io/native-build-tools/latest/maven-plugin.html). The simple Test class is very useful to build native image configuration using the GraaalVM native agent.

    ![Docker Minimal JRE Image Snapshot]()

    2. **server_native_image**: Native _java_ application
