# DIME-Connector.Docker
Running DIME Connector in Docker

```sh
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
cp -r DIME-Connector.Docker/ConfigExample/* volumes/dime/connector/configs

# load image
docker pull datainmotionenterprise/connector:latest
docker images

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

