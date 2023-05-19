Pad协议教程

1. [pad-local](http://pad-local.com/) 获取PadLocal Token

2. Python随机生成UUID：
   import uuid;
   print(uuid.uuid4());

3. Docker容器部署Padlocal网关服务(代码在最下方，替换
   WECHATY_PUPPET_PADLOCAL_TOKEN 和 WECHATY_TOKEN为实际值)

4. 将uuid配置在config.json(对应KEY:wechaty_puppet_service_token)

   ，docker-compose的话，写在docker-compose.yaml文件里

5. 修改启动文件app.py
   channel = channel_factory.create_channel("wxy")

   （docker-compose的话，在docker-compose.yaml取消掉channel_type的注释）

*备注：

1. Install：pip3 install wechaty
2. 配置文件 config.json 内的 **wechaty_puppet_service_token** 非[pad-local](http://pad-local.com/) 获取的Token，此处的token为uuid生成的，一定要将uuid生成的token和在pad-local获取到的token部署在Docker网关内！！！！
3. 判断环境是否存在问题，可以运行一下官方示例][ding-dong-bot.py](https://github.com/wechaty/python-wechaty/blob/master/examples/ding-dong-bot.py)，具体[中文文档](https://wechaty.readthedocs.io/zh_CN/latest/)。
4. 本地运行没有公网IP，需要将 **os.environ['WECHATY_PUPPET_SERVICE_TOKEN'] = token** 修改为 **os.environ['WECHATY_PUPPET_SERVICE_ENDPOINT'] = "127.0.0.1:9001"**（这里是修改源代码）

```
# 设置环境变量
export WECHATY_LOG="verbose"
export WECHATY_PUPPET="wechaty-puppet-padlocal"
# PadLocal Token
export WECHATY_PUPPET_PADLOCAL_TOKEN="puppet_padlocal_xxx"

export WECHATY_PUPPET_SERVER_PORT="9001"
# 可使用代码随机生成UUID：import uuid;print(uuid.uuid4());
export WECHATY_TOKEN="d671a197-71c9-4ca6-a673-xxxxxx"
# 由于版本细节问题，目前python-wechaty 支持最好的wechaty镜像为：[wechaty/wechaty:0.65](https://hub.docker.com/layers/wechaty/wechaty/0.65/images/sha256-d39b9fb5dece3a8ffa88b80a8ccfd916be14b9d0de72115732c3ee714b0d6a96?context=explore)
docker run -tid \
  --name wechaty_puppet_service_token_gateway \
  --rm \
  -e WECHATY_LOG \
  -e WECHATY_PUPPET \
  -e WECHATY_PUPPET_PADLOCAL_TOKEN \
  -e WECHATY_PUPPET_SERVER_PORT \
  -e WECHATY_TOKEN \
  -p "$WECHATY_PUPPET_SERVER_PORT:$WECHATY_PUPPET_SERVER_PORT" \
  wechaty/wechaty:0.65
```

Pad协议教程

1. [pad-local](http://pad-local.com/) 获取PadLocal Token
2. Python随机生成UUID：
   import uuid;
   print(uuid.uuid4());
3. Docker容器部署Padlocal网关服务(代码在最下方，替换
   WECHATY_PUPPET_PADLOCAL_TOKEN 和 WECHATY_TOKEN为实际值)
4. 将uuid配置在config.json(对应KEY:wechaty_puppet_service_token)
5. 修改启动文件app.py
   channel = channel_factory.create_channel("wxy")

*备注：

1. Install：pip3 install wechaty
2. 配置文件 config.json 内的 **wechaty_puppet_service_token** 非[pad-local](http://pad-local.com/) 获取的Token，此处的token为uuid生成的，一定要将uuid生成的token和在pad-local获取到的token部署在Docker网关内！！！！
3. 判断环境是否存在问题，可以运行一下官方示例][ding-dong-bot.py](https://github.com/wechaty/python-wechaty/blob/master/examples/ding-dong-bot.py)，具体[中文文档](https://wechaty.readthedocs.io/zh_CN/latest/)。
4. 本地运行没有公网IP，需要将 **os.environ['WECHATY_PUPPET_SERVICE_TOKEN'] = token** 修改为 **os.environ['WECHATY_PUPPET_SERVICE_ENDPOINT'] = "127.0.0.1:9001"**

```
# 设置环境变量
export WECHATY_LOG="verbose"
export WECHATY_PUPPET="wechaty-puppet-padlocal"
# PadLocal Token
export WECHATY_PUPPET_PADLOCAL_TOKEN="puppet_padlocal_xxx"

export WECHATY_PUPPET_SERVER_PORT="9001"
# 可使用代码随机生成UUID：import uuid;print(uuid.uuid4());
export WECHATY_TOKEN="d671a197-71c9-4ca6-a673-xxxxxx"
# 由于版本细节问题，目前python-wechaty 支持最好的wechaty镜像为：[wechaty/wechaty:0.65](https://hub.docker.com/layers/wechaty/wechaty/0.65/images/sha256-d39b9fb5dece3a8ffa88b80a8ccfd916be14b9d0de72115732c3ee714b0d6a96?context=explore)
docker run -ti \
  --name wechaty_puppet_service_token_gateway \
  --rm \
  -e WECHATY_LOG \
  -e WECHATY_PUPPET \
  -e WECHATY_PUPPET_PADLOCAL_TOKEN \
  -e WECHATY_PUPPET_SERVER_PORT \
  -e WECHATY_TOKEN \
  -p "$WECHATY_PUPPET_SERVER_PORT:$WECHATY_PUPPET_SERVER_PORT" \
  wechaty/wechaty:0.65
  
  
  
  docker logs -f wechaty_puppet_service_token_gateway 查看日志
```

