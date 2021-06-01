# kitty-blaster

:gun: :scream_cat:

An exercise in load testing using [Gatling](https://gatling.io/).

Prerequisites:

- [Docker Compose](https://docs.docker.com/compose/install/)
- [JDK8](https://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)
- [Maven](https://maven.apache.org/install.html)
- [Gatling](https://gatling.io/docs/current/installation/#installation)

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

Check that everything is working by navigating to the UI's [cats](http://localhost:2997/cats) view.

Download the Gatling bundle to a directory of your choice and unzip it.

```shell
export DIR=/path/to/gatling/bundle
curl -o $DIR/gatling-bundle.zip \
https://repo1.maven.org/maven2/io/gatling/highcharts/gatling-charts-highcharts-bundle/3.6.0/gatling-charts-highcharts-bundle-3.6.0-bundle.zip
unzip $DIR/gatling-bundle.zip -d $DIR
```

Now examine the Gatling [simulation](./gatling-simulations/UI2APILoadTest.scala) for load testing the UI and API components together.

Copy our simulation to the bundle's simulations directory and run Gatling.

```shell
cp gatling-simulations/UI2APILoadTest.scala $DIR/gatling-charts-highcharts-bundle-3.6.0/user-files/simulations/
$DIR/gatling-charts-highcharts-bundle-3.6.0/bin/gatling.sh
```

Run the simulation by selecting the corresponding number from the list presented by Gatling on startup.

Gatling will generate an HTML report once the simulation has finished and output a path to the report file.

Open this file in your browser and analyze the report. Look for areas where service performance could be improved, for example the 3 slowest calls. Bear in mind that load testing services running on your local machine will not produce results representitive of how these services will perform when deployed in a production environment with significantly more resources allocated to them.
