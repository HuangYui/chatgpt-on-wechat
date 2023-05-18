##### 前置

- 请先自己配置好一个代理
- 有自己的API KEY



##### 开始部署

1. 打开Docker目录下的docker-compose.yaml，修改以下参数:

   

   ```java
   OPEN_AI_API_KEY
   OPEN_AI_PROXY
   PROXY
   ```

   例如：

   ```java
   version: '2.0'
   services:
     chatgpt-on-wechat:
       build:
         context: ./
         dockerfile: Dockerfile.alpine
         args:
           PROXY: 'http://172.17.0.1:7890'
       image: zhayujie/chatgpt-on-wechat
       container_name: sample-chatgpt-on-wechat
       environment:
         OPEN_AI_API_KEY: 'xxxxx'
         OPEN_AI_PROXY: 'http://172.17.0.1:7890'
         SINGLE_CHAT_PREFIX: '["bot", "@bot"]'
         SINGLE_CHAT_REPLY_PREFIX: '"[bot] "'
         GROUP_CHAT_PREFIX: '["@bot"]'
         GROUP_NAME_WHITE_LIST: '["ChatGPT测试群", "ChatGPT测试群2"]'
         IMAGE_CREATE_PREFIX: '["画", "看", "找"]'
         CONVERSATION_MAX_TOKENS: 1000
         SPEECH_RECOGNITION: "False"
         CHARACTER_DESC: '你是ChatGPT, 一个由OpenAI训练的大型语言模型, 你旨在回答并解决人们的任何问题，并且可以使用多种语言与人交流。'
         EXPIRES_IN_SECONDS: 3600
         DEBUG: "true"
         OPEN_AI_BASE: "https://api.openai.com/v1"
         request_timeout: 60
   ```

   

2. 修改docker目录下，config-template.json参数

   ```java
   这里只需要修改proxy即可
   "proxy": "http://172.17.0.1:7890"
   ```

##### 启动

```bash
docker-compose up -d --build
查看日志，并扫描二维码即可：
docker logs -f sample-chatgpt-on-wechat 
```



