
# 流管理系统API文档

## 一般规则

所有交互使用HTTP REST方式交互。

* HOST: `interface.qietv.douyucdn.cn`
* 端口: `80` 或 `443(SSL)`
* 非特定约定使用 HTTP POST方式
* 数据交换方式: JSON 

## 消息体格式

### 请求

> 使用将各个参数放入标准JSON的Field即可。

* 下面的为标准的请求消息体格式：
```json
{
    "vid":10454
}
```

### 应答

> 接收消息格式为JSON

| 属性           |    类型        |  内容值                     |          备注            |
|---------------|----------------|-----------------------------|-------------------------|
| code          |     Integer     | 消息类型，类似于http cod    | 必须                     |
| message       |     String     |      错误或者成功信息         | 必须                     |
| data          |      Object<T>  |     数据                    | Json Object             |

* 下面的为标准的应答消息体格式：
```json
{
    "code":200,
    "message":"SUCCESS",
    "result":{
        "stream":{
            "streamName":"10002625rATSDQFg",
            "imageKey":"0a7e82c9085134fc10d4c6eea2fd2252",
            "image":0,
            "roomId":"10002625",
            "categoryName":"足球",
            "cdnType":0,
            "imageCdnType":99,
            "imageUrl":"http://rpic.qietv.douyucdn.cn/z1610/20/18/10002625_161020182409.jpg",
            "p2p":false,
            "userName":"安哥拉男子足球队",
            "endTime":1477111020388,
            "startTime":1477068624056,
            "duration":41686240,
            "type":0,
            "cdnEndTime":1477111020388,
            "mp4":false,
            "userId":3813709,
            "checkStatus":0,
            "flv":false,
            "cdnStartTime":1477068624056,
            "title":"【阿森纳】 纪录片+高清比赛",
            "categoryId":198,
            "m3u8":true,
            "bucket":"qietv-rec",
            "persistentId":"1005aa2afb6b153840608cbe2c9a00ee5f0b",
            "clear":30,
            "status":100,
            "file":false,
            "resourceId":13113
        },
        "videos":[
            {
                "hash":"Frx0deIRkab_p11yA1tQFo7LZY4s",
                "fileSize":127296,
                "height":0,
                "streamName":"10002625rATSDQFg",
                "cdnType":0,
                "seq":0,
                "duration":41672355,
                "type":3,
                "recordId":13113,
                "key":"m3u8/20161022/live-10002625rATSDQFg--20161022005023-1080.m3u8",
                "bucket":"qietv-video-play",
                "persistentId":"10054003f8747bb84e28ba7ec0fcfc263b08",
                "width":0,
                "clear":30,
                "resourceId":20506
            },
            {
                "hash":"FiUgXT7ax0zr99nEeoZtZphUVCM9",
                "fileSize":127296,
                "height":1080,
                "streamName":"10002625rATSDQFg",
                "cdnType":0,
                "seq":0,
                "duration":41686240,
                "type":3,
                "recordId":13113,
                "key":"m3u8/20161022/live-10002625rATSDQFg--20161022005023-720.m3u8",
                "bucket":"qietv-video-play",
                "persistentId":"10054003f8747bb84e28ba7ec0fcfc263b08",
                "width":1280,
                "clear":20,
                "resourceId":20504
            },
            {
                "hash":"FtBzdciC51se3c47qQz7H63f4lk1",
                "fileSize":127296,
                "height":1080,
                "streamName":"10002625rATSDQFg",
                "cdnType":0,
                "seq":0,
                "duration":41686240,
                "type":3,
                "recordId":13113,
                "key":"m3u8/20161022/live-10002625rATSDQFg--20161022005023-480.m3u8",
                "bucket":"qietv-video-play",
                "persistentId":"10054003f8747bb84e28ba7ec0fcfc263b08",
                "width":853,
                "clear":10,
                "resourceId":20505
            }
        ]
    }
}
```

## 直播状态上报

> 向流管理服务器上报开关播信息

### 开播

* URL ```http://{HOST:PORT}/api/v1/live/start```

* 参数 ```startTime``` ```categoryId``` ```categoryName``` ```userId``` ```userName``` ```title``` ```roomId``` ```ip```

| 字段名         |        类型         | 备注                      | 必须  |
|---------------|---------------------|---------------------------|-------|
| startTime     |        long         | 开播当时服务器的UINX时间戳  |  是   |
| categoryId    |        int          |     分类ID                |  是   |
| categoryName  |       string        |     分类名                |  否   |
| userId        |         int         |     用户ID                |  是   |
| userName      |       string        |     用户名                 |  是   |
| title         |       string        |     当时直播间名字          |  是   |
| roomId        |       string        |     房间ID                 |  是   |
| ip            |       string        |     用户ip                 |  是   |

* 返回：

```json
{
    "code":200,
    "message":"SUCCESS",
    "result":"OK"
}
```
