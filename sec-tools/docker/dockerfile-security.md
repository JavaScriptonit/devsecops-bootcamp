https://coursehunter.net/course/devsecops-bootcamp?lesson=41

# Best Practices building Dockerfile:

1. ## Use ready official IMAGE instead of many STEPS with downloading packages
    1. Example:
    ```
    FROM node:14
    ```
    2. Example: 
    ```
    FROM ubuntu:20.04
    RUN apt-get update && apt-get install -y \
        curl \
        gnupg \
        && curl -sL https://deb.nodesource.com/setup_14.x | bash - \
        && apt-get install -y nodejs \
    ```
2. ## Use tags instead of `node:latest`:
    1. Example:
    ```
    FROM node:14
    ```
3. ## Use different operating systems (ubuntu/debian/centos) and different versions of programs:
    1. Example (with LEANER & SMALLER OS distro) - 48.32MB. Less packages = more secure image:
    ```
    FROM node:17.0.1-alpine
    ```
    2. Example (full-blown OS) - 351.24MB:
    ```
    FROM node:17.0.1
    ```
4. ## Use Alpine Linux when no need of concrete OS:
    1. Lightweight Linux distro
    2. Security-oriented
    3. Popular base image
5. ## Create .dockerignore file:
    1. Ignore `.git, .cache, *.md, private.key, settings.json`
6. ## Multi-Stage Builds:
    1. Separate the build tools and dependencies from a runtime:
    ```
    # Build stage
    FROM maven AS build
    WORKDIR /app
    COPY myapp /app
    RUN mvn package

    # Run stage
    FROM tomcat
    COPY --from=build /app/target/file.war /usr/local/tomcat/
    ```
    2. Less packages = Lightweight image = more secure image
7. ## Use the Least Privileged User:
    1. Create a dedicated user and group (create/set permissions/switch):
    ```
    RUN groupadd -r tom && useradd -g tom tom
    RUN chown -R tom:tom /app
    USER tom
    CMD node index.js
    ```
    2. Some Base Images have a generic user bundled in: No need to create another:
    ```
    FROM node:10-alpine
    USER node
    CMD node index.js
    ```