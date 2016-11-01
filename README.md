# comment-doc
弹幕系统中文文档(MQ版本)

## 发送弹幕流程

#### 连接MQ服务器

> 弹幕地址 (MQ服务器公网)
```
123.59.101.208:5672
```

> 弹幕地址 (MQ服务器内网)
```
172.18.130.148:5672
```

#### 确定交换机

> 发送评论交换机

| 选项           |     英文项     | 值                          |    备注  |
|---------------|----------------|-----------------------------|---------|
| 交换机名称     |      name      | send-comment               | string     |
| 模式          |     mode        |      direct                 | enum     |
| 持久化        |      durable    |           true              | boolean     |
| 自动删除       |    autoDelete  |          false               | boolean     |

#### 确定发送评论队列

> 发送评论队列

| 选项           |       英文项        | 值                                   | 备注  |
|---------------|---------------------|-------------------------------------|---------|
| 队列名称     |      name           |     comment.send               | string  |
| 路由          |     rotingKey            |      comment.send             |  string   |
| 持久化        |      durable        |           true                      |  boolean |
| 自动删除       |     autoDelete     |           false                      |  boolean |

#### 发送评论

评论为普通JSON
> 伪代码(Kotlin)
```
data class Comment(var content:String,var ct:Int,var did:String,var icon:String,var ip:String,var nick:String,var pg:Int,var rg:Int,var ts:Long,var uid:Int,var sts:Long = 0,var type:Int = 0,var room:String = "") {
}
```


| 字段名         |        类型         | 备注                      | 必须  |
|---------------|---------------------|---------------------------|-------|
| content       |      string         |     弹幕内容               |  是   |
| ct            |      int            |     平台类型               |  是   |
| did           |      string         |     上条弹幕(.?)           |  是   |
| icon          |      string         |     弹幕图片               |  是   |
| ip            |      string         |     用户IP                 |  是   |
| nick          |      string         |     用户昵称               |  是   |
| pg            |      int            |     平台权限组              |  是   |
| rg            |      int            |     房间权限组              |  是   |
| ts            |     long            |     当前时间戳             |  是   |
| uid           |     int             |     用户ID                 |  是   |
| sts           |     long            |     当前播放时间轴          |  是   |
| type          |     int             |     弹幕类型                |  是   |
| room          |     string          |     房间号                  |  是   |


## 接收弹幕
### 服务器经过关键字过滤、弹幕入库等操作后，将向广播交换机广播弹幕，从服只需要将任意队列绑定到交换机上获取弹幕即可
#### 确定交换机

> 接受评论(广播)交换机 

| 选项           |       英文项        | 值                                   | 备注  |
|---------------|---------------------|-------------------------------------|---------|
| 交换机名称     |      name           |     broadcast-comment               | string  |
| 模式          |     mode            |              fanout                 |  enum   |
| 持久化        |      durable        |           true                      |  boolean |
| 自动删除       |     autoDelete     |           false                      |  boolean |

#### 将队列绑定到交换机，因为是广播模式 因此队列路由key自行设置，建议使用UUID或者从服务器名字等不易重复的值

> 发送评论队列(建议)

| 选项           |       英文项        | 值                                   | 备注  |
|---------------|---------------------|-------------------------------------|---------|
| 队列名称     |      name           |     UUID.randomUUID.toString()        | string  |
| 持久化        |      durable        |           true                      |  boolean |
| 自动删除       |     autoDelete     |           false                     |  boolean |

接收弹幕伪代码(Kotlin)

```kotlin
@RabbitListener(bindings = arrayOf(QueueBinding(Queue(), exchange = Exchange(Constants.BROADCAST_COMMENT_EXCHANGE,type = "fanout",durable = "true",autoDelete = "false"))))
fun receiveFooQueue(foo: Comment) {
    log.info("Received {}",JacksonHelper.toJSON(foo))
    //logger.info("Received Message <${foo.size}>")
}
```
