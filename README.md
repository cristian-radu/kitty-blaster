# kitty-blaster

:gun: :scream_cat:

An exercise in load testing using [Gatling](https://gatling.io/).

Prerequisites:

- [Docker Compose](https://docs.docker.com/compose/install/)
- [Maven](https://maven.apache.org/install.html)

This project imports [animals-api](https://github.com/catapultcx/animals-api) and [animals-ui](https://github.com/catapultcx/animals-ui) as git submodules.

Initialize and update the two submodules.

```shell
git submodule init
git submodule update
```

Build the animals API from source.

```shell
mvn clean package -f animals-api/pom.xml
```

Build docker images for the animals API and UI components.

```shell
docker-compose build
```

Start the two services in the background.

```shell
docker-compose up -d
```

Check that everything is working by navigating to the UI's [cats](http://localhost:2997/cats) view. You should see a table containing cat names and descriptions.
