# Instructions

## Index

* [ Setup ](#setup)
  * [ Build ](#build)
  * [ Run ](#run)

## Setup

### Build

Copy the **liferay-dxp-tomcat-7.1.10.1-sp1-20190110085705206.zip** package into the dxp folder:

```
cp liferay-dxp-tomcat-7.1.10.1-sp1-20190110085705206.zip dxp/
```

Copy the Liferay DXP 7.1 license into the dxp folder (and rename to license.xml):

```
cp activation-key-development-xyz.xml dxp/license.xml
```

Copy the Liferay DXP 7.1 last fixpack named **liferay-fix-pack-dxp-6-7110.zip** into the dxp directory:

```
cp liferay-fix-pack-dxp-6-7110.zip dxp/
```

Build:

```
docker-compose build
```

### Run

Run the docker compose for DXP Cluster:

```
docker-compose up -d
```

Go to http://localhost:8080 and login as admin (test/test).

Watch the logs:

```
docker logs -f dxp
```


Reindex all search indexes.

Install your plugins and enjoy. ;)
