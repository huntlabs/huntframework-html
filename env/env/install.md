# hunt 安装指南

#### 安装 dub
hunt框架使用[dub](https://dlang.org/download.html)来管理依赖,所以在你使用hunt之前,必须确保dub正确安装


#### 安装 hunt
使用dub工具:
- 新建项目目录
- 进入到项目目录执行dub init
- 编辑dub.json,添加如下配置
```json
    "dependencies": {
        "hunt":"~>0.8.5"
    }
    "configurations": [{
        "name": "default",
        "subConfigurations": {
            "hunt": "default"
        }
    }]
```

- 执行dub build -f -v 重新编译项目
