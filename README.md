# Keycloak Docker image

## How the image is build

This image uses the keycloak [repository](https://github.com/keycloak/keycloak-containers) that is used to build the original JBoss Keycloak image. The only diference is that the Dockerfile used to build the "original" version of keycloak is changed with the one from this repository and the image is build on a Raspberry Pi 3 (32 bit)

## How to use

The documentation for using the image can be found [here](https://hub.docker.com/r/jboss/keycloak). It is exactly the same so as a refrence you can use that documentation to start your keycloak image on your shiny ARM processor

