# Javalin-Native-Image-Example
Create a minimal native application around a Maven project using GraalVM Maven plugin project and ship it as ***super lightweight*** Docker image 

 ![Docker Images Snapshot](https://github.com/newfla/Javalin-Native-Image-Example/blob/main/res/docker_images_comparison.png?raw=true) 

## Repository content
- **/server** folder contains a modified Maven pom file for the [Javalin Hello-World example](https://github.com/newfla/Create-JRE-using-Docker).
The code is packaged as single Fat-Jar using the [maven-shade-plugin](https://maven.apache.org/plugins/maven-shade-plugin/)

- **Dockerfile** describes *2* images based on [Ubuntu 22.04 docker image](https://hub.docker.com/layers/library/ubuntu/jammy/images/) and [GraalVM CE JDK](https://github.com/oracle/graal/):

    1. **server_builder**: builds the maven project and creates the native image using the [GraalVM native Image Maven plugin](https://graalvm.github.io/native-build-tools/latest/maven-plugin.html). The simple Test class is very useful to build native image configuration using the GraaalVM native agent.
    Configuration files are moved into META-INF/native-image in the fat-jar and then used to build a functional Javalin native-image

    ![Docker Minimal JRE Image Snapshot](https://github.com/newfla/Javalin-Native-Image-Example/blob/main/res/dockerfile.png?raw=true)

    2. **server_native_image**: Ubuntu + java native-image application


# Size reduction
| Image  | Size  | vs JDK | vs JRE  | vs Native |
|--------|-------|--------|---------|-----------|
| JDK    | 835MB | -      | 618%    | 810%      |
| JRE    | 135MB | 16%    | -       | 131%      |
| Native | 103MB | 12%    | 76%     | -         |
    
**The native Image is 24% smaller than the optimized-jre one**

# Start-up time reduction

| Image  | Time  | vs JDK | vs JRE  | vs Native |
|--------|-------|--------|---------|-----------|
| JDK    | 502ms | -      | 127%    | 1434%     |
| JRE    | 395ms | 78%    | -       | 1128%     |
| Native | 35ms  | 7%     | 8%      | -         |

**The native Image is 92% faster to start-up than the optimized-jre one**
