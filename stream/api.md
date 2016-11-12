
# 流管理系统API文档

## 一般规则

所有交互使用HTTP REST方式交互。

* HOST: `interface.qietv.douyucdn.cn`
* 端口: `80` 或 `443(SSL)`
* 非特定约定使用 HTTP POST方式
* 数据交换方式: JSON 

## 消息体格式

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
