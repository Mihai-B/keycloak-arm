# Keycloak Docker image

**docker hub:** [![Docker Pulls](https://img.shields.io/docker/pulls/mihaibob/keycloak.svg)](https://hub.docker.com/r/mihaibob/keycloak) 
<br>
**buy me a coffe:** [![Buy a coffe](https://cdn.rawgit.com/twolfson/paypal-github-button/1.0.0/dist/button.svg)](https://www.paypal.com/paypalme2/mihaibob/1?locale.x=en_US)

## Available Keycloak versions
### ARM

10.x: 10.0.2 <br>
11.x: 11.0.0, 11.0.1, 11.0.2, 11.0.3 <br>
12.x: 12.0.1, 12.0.2, 12.0.4 <br>
13.x: 13.0.0, 13.0.3 <br>
14.x: 14.0.0 <br>

### ARM 64
- need help at this part as I personally do not have a ARM64 board

## How the image is build

This image uses the official Keycloak [repository](https://github.com/keycloak/keycloak-containers) that is used to build the official Keycloak image. The only difference is that the Dockerfile used to build the official version of Keycloak is changed with the one from [this](https://github.com/Mihai-B/keycloak-arm) repository and the image is build on a Raspberry Pi 3 (32 bit)

The docker image has to be changed when building the ARM version of Keycloak because the base image that is used by Keycloak does not support ARM processors thus it is swapped with Ubuntu as base image

## How to use

### Quick start Keycloak using MySql/MariaDb

#### First run
`docker run -p 9877:8080 --name keycloak -e KEYCLOAK_USER=<ADMIN_USERNAME> -e KEYCLOAK_PASSWORD=<ADMIN_PASS>  -e DB_VENDOR=<DB_VENDOR> -e DB_ADDR=<DB_ADDRESS> -e DB_DATABASE=<DATABASE_NAME> -e DB_USER=<DATABASE_USER> -e DB_PASSWORD=<DATABASE_PASS> -e JDBC_PARAMS: "serverTimezone=UTC" mihaibob/keycloak:<KEYCLOAK_VERSION>`

In this example Keycloak will be available on port 9877. <br>
The variables need to be changed acordingly: <br>
ADMIN_USERNAME - the username you want to use for Keycloak's admin user <br>
ADMIN_PASS - the password for Keycloak's admin user <br>
DB_VENDOR - the database vendor, can be any of: h2, mysql, mariadb, postgres, oracle, mssql <br>
DB_ADDRESS - where the database can be accessed, example: 192.168.1.10. Do not use 'localhost' even if the database is on the same raspberry pi <br>
DATABASE_NAME - the database keycloak should create the tables in(make sure the database is allready created) <br>
DATABASE_USER - the user that keycloak should use to access the database <br>
DATABASE_PASS - the password keycloak should use to access the database <br>
KEYCLOAK_VERSION - the Keycloak version to run

#### Upgrading Keycloak container to a later version

After Keycloak was run using the 'First run' command, and an upgrade is in order then the command to start Keycloak should look like this:
`docker run -p 9877:8080 -d --name keycloak -e DB_VENDOR=mysql -e DB_ADDR=<DB_ADDRESS> -e DB_DATABASE=<DATABASE_NAME> -e DB_USER=<DATABASE_USER> -e DB_PASSWORD=<DATABASE_PASS> -e JDBC_PARAMS: "serverTimezone=UTC" mihaibob/keycloak:<KEYCLOAK_VERSION>`

Notice we did not specify the 'KEYCLOAK_USER' and 'KEYCLOAK_PASSWORD' since they are saved in the database now

### Full documentation 
For a complete documentation refer to Keycloak's official documentation on how to use the docker image because this image will work exactly the same. The documentation can be found [here](https://hub.docker.com/r/jboss/keycloak).
