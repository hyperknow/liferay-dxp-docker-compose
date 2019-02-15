# Instructions

## Index

* [ Setup ](#setup)
  * [ Build ](#build)
  	* [ Docker Images ](#docker-images)
    	* [ Java Base Layer ](#java-base-layer)
    	* [ Elasticsearch ](#elasticsearch)
    	* [ Liferay DXP 7.1 ](#liferay-dxp-7.1)
  * [ Run ](#run)


## Setup

### Build

#### Java Base Layer

Go to java folder and build the image:

```
cd java/
docker build -t lfrdxp/java-base . 
```

#### Elasticsearch

Go to els directory and build the image:

```
cd els
docker build -t lfrdxp/elasticsearch .
```

#### Liferay DXP 7.1

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

Build the DXP 7.1 image:

```
cd dxp/
docker build -t lfrdxp/dxp .
```

### Run

Run the docker compose for DXP Cluster:

```
docker-compose up -d
```

Go to http://localhost:8080 and login as admin (test/test).

Reindex all search indexes.

Install your plugins and enjoy. ;)
