# yapi

[![Build Status](https://cloud.drone.io/api/badges/v7lin/yapi/status.svg)](https://cloud.drone.io/v7lin/yapi)
[![Docker Pulls](https://img.shields.io/docker/pulls/v7lin/yapi.svg)](https://hub.docker.com/r/v7lin/yapi)

### 项目源码

[YMFE/yapi](https://github.com/YMFE/yapi)

### 用法示例

````
# 版本
version: "3.7"

# 服务
services:

  mongo:
    container_name: mongo
    image: mongo:2.6
    restart: always
    hostname: mongo
#    ports:
#      - 27017
    volumes:
      - ../dev-ops-repo/yapi/mongo:/data/db
    environment:
      - TZ=${TIME_ZONE:-Asia/Shanghai}

  yapi:
    container_name: yapi
    image: v7lin/yapi
    restart: always
    hostname: yapi
    ports:
      - 8080:3000
    volumes:
      - ../dev-ops-repo/yapi/init:/yapi/init
#      - ../dev-ops-repo/yapi/log:/yapi/log
    environment:
      - TZ=${TIME_ZONE:-Asia/Shanghai}
      - YAPI_PORT=3000
      - YAPI_CLOSEREGISTER=true # 关闭注册
      - YAPI_ADMINACCOUNT=yapi@yapi.com # 管理员帐号
      - YAPI_ADMINPASSWORD=yapi # 管理员初始化密码
      - YAPI_DB_SERVERNAME=mongo # mongo 数据库地址
      - YAPI_DB_PORT=27017 # mongo 数据库端口
      - YAPI_DB_DATABASE=yapi # mongo 数据库名
    depends_on:
      - mongo
````
