# Instructions

## Index

* [ Setup ](#setup)
  * [ Build ](#build)
  * [ Run ](#run)

## Setup

### Build

Copy the **liferay-dxp-digital-enterprise-7.0-sp6-fp39.zip** package into the dxp folder:

```
cp liferay-dxp-digital-enterprise-7.0-sp6-fp39.zip dxp/
```

Copy the Liferay DXP 7.0 license into the dxp folder (and rename to license.xml):

```
cp activation-key-digitalenterprisedevelopment-7.0-sisallotteryportalmarocc....xml dxp/license.xml
```

Build:

```
docker-compose build
```

### Run

Run the docker compose for DXP:

```
docker-compose up -d
```

Watch the logs:

```
docker logs -f dxp
```

Go to http://<local ip>:8080 and login as admin (test/test).



Install your plugins and enjoy. ;)
