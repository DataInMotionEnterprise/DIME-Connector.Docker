# DIME-Connector.Docker
Running DIME Connector in Docker

# General

```sh
CONFIG=Basic

cd ~

# clone repostitory
git clone https://github.com/DataInMotionEnterprise/DIME-Connector.Docker

# create volumes
mkdir -p volumes/dime/connector/configs
mkdir -p volumes/dime/connector/lua
mkdir -p volumes/dime/connector/python
mkdir -p volumes/dime/connector/logs

# copy artifacts
cp DIME-Connector.Docker/nlog.config volumes/dime/connector/nlog.config
cp -r DIME-Connector.Docker/Lua/* volumes/dime/connector/lua
cp -r DIME-Connector.Docker/Python/* volumes/dime/connector/python
cp -r DIME-Connector.Docker/Configs/${CONFIG}/* volumes/dime/connector/configs

# run container
docker run \
   -p 5000:5000 \
   -p 7878:7878 \
   -p 8080:8080 \
   -p 8081:8081 \
   -p 8082:8082 \
   -p 9998:9998 \
   -p 9999:9999 \
   -v ~/volumes/dime/connector/nlog.config:/app/nlog.config \
   -v ~/volumes/dime/connector/configs:/app/Configs \
   -v ~/volumes/dime/connector/lua:/app/Lua \
   -v ~/volumes/dime/connector/python:/app/Python \
   -v ~/volumes/dime/connector/logs:/app/Logs \
   --rm
   datainmotionenterprise/connector:latest
```

## ROS2

```sh
CONFIG=Ros2Subscription

cd ~

# clone repostitory
git clone https://github.com/DataInMotionEnterprise/DIME-Connector.Docker

# create volumes
mkdir -p volumes/dime/connector/configs
mkdir -p volumes/dime/connector/lua
mkdir -p volumes/dime/connector/python
mkdir -p volumes/dime/connector/logs

# copy artifacts
cp DIME-Connector.Docker/nlog.config volumes/dime/connector/nlog.config
cp -r DIME-Connector.Docker/Lua/* volumes/dime/connector/lua
cp -r DIME-Connector.Docker/Python/* volumes/dime/connector/python
cp -r DIME-Connector.Docker/Configs/${CONFIG}/* volumes/dime/connector/configs

# run container
docker run \
   -v ~/volumes/dime/connector/nlog.config:/app/nlog.config \
   -v ~/volumes/dime/connector/configs:/app/Configs \
   -v ~/volumes/dime/connector/lua:/app/Lua \
   -v ~/volumes/dime/connector/python:/app/Python \
   -v ~/volumes/dime/connector/logs:/app/Logs \
   --network host \
   --ipc host \
   --pid host \
   --rm \
   datainmotionenterprise/connector:latest-ros2
```

## Splunk Edge Hub

### OTI Deployment

[Splunk OTI Documentation](https://help.splunk.com/en/data-management/splunk-ot-intelligence/set-up-splunk-ot-intelligence/4.12/use-splunk-ot-intelligence/deploy-and-configure-docker-containers-in-splunk-ot-intelligence)

JSON Configuration  

```json
{
  "portMap": ["51000:7878", "51001:8080", "51002:8081", "51003:8082", "51004:8092", "51999:9998", "52000:9999"],
  "mappedStorage": "/app/Configs"
}
```

[Example DIME Configuration](./Configs/SplunkEdgeHubSingleFileV2/main.yaml)

### Edge Hub Deployment

[Splunk Edge Hub Documentation](https://help.splunk.com/en/splunk-cloud-platform/ot-intelligence/administer-splunk-edge-hub-os/2.0/configure-advanced-settings/use-docker-containers-with-splunk-edge-hub-os)

Use the pre-built Splunk tarball.  

```sh
VERSION=3.0.0

https://github.com/DataInMotionEnterprise/DIME-Releases/releases/download/connector-${VERSION}/dime-connector-splunk-${VERSION}.tar
```

[Example DIME Configuration](./Configs/SplunkEdgeHubSingleFileV2/main.yaml)