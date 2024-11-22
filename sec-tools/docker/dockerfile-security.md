https://coursehunter.net/course/devsecops-bootcamp?lesson=41

# Best Practices building Dockerfile:

1. Use ready official IMAGE instead of many STEPS with downloading packages
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
2. Use tags instead of `node:latest`:
    1. Example:
    ```
    FROM node:14
    ```
3. 