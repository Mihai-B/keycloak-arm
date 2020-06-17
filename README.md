# Keycloak Docker image

**docker hub:** [![Docker Pulls](https://img.shields.io/docker/pulls/rat2000/keycloak.svg)](https://hub.docker.com/r/rat2000/keycloak) 
<br>
**buy me a coffe:** [![Buy a coffe](https://cdn.rawgit.com/twolfson/paypal-github-button/1.0.0/dist/button.svg)](https://www.paypal.com/paypalme2/mihaibob/1?locale.x=en_US)

## Available Keycloak versions
### ARM

8.x: 8.0.0, 8.0.2 <br>
9.x: 9.0.0, 9.0.2, 9.0.3 <br>
10.x: 10.0.2

### ARM 64
- need help at this part as I personally do not have a ARM64 board

## How the image is build

This image uses the keycloak [repository](https://github.com/keycloak/keycloak-containers) that is used to build the original JBoss Keycloak image. The only diference is that the Dockerfile used to build the "original" version of Keycloak is changed with the one from [this](https://github.com/Mihai-B/keycloak-arm) repository and the image is build on a Raspberry Pi 3 (32 bit)

## How to use

### Quick start Keycloak using MySql/MariaDb

#### First run
`docker run -p 9877:8080 --name keycloak -e KEYCLOAK_USER=<ADMIN_USERNAME> -e KEYCLOAK_PASSWORD=<ADMIN_PASS>  -e DB_VENDOR=<DB_VENDOR> -e DB_ADDR=<DB_ADDRESS> -e DB_DATABASE=<DATABASE_NAME> -e DB_USER=<DATABASE_USER> -e DB_PASSWORD=<DATABASE_PASS> rat2000/keycloak:<KEYCLOAK_VERSION>`

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
`docker run -p 9877:8080 -d --name keycloak -e DB_VENDOR=mysql -e DB_ADDR=<DB_ADDRESS> -e DB_DATABASE=<DATABASE_NAME> -e DB_USER=<DATABASE_USER> -e DB_PASSWORD=<DATABASE_PASS> rat2000/keycloak:<KEYCLOAK_VERSION>`

### Full documentation 
For a complete documentation refer to the JBoss Keycloak's official documentation on how to use the docker image. The documentation can be found [here](https://hub.docker.com/r/jboss/keycloak).


