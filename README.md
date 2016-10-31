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

> 接受评论(广播)交换机

| 选项           |       英文项        | 值                                   | 备注  |
|---------------|---------------------|-------------------------------------|---------|
| 交换机名称     |      name           |     broadcast-comment               | string  |
| 模式          |     mode            |              direct                 |  enum   |
| 持久化        |      durable        |           true                      |  boolean |
| 自动删除       |     autoDelete     |           true                      |  boolean |

#### 确定发送评论队列

> 发送评论队列

| 选项           |       英文项        | 值                                   | 备注  |
|---------------|---------------------|-------------------------------------|---------|
| 队列名称     |      name           |     comment.send               | string  |
| 路由          |     rotingKey            |      comment.send                       |  string   |
| 持久化        |      durable        |           true                      |  boolean |
| 自动删除       |     autoDelete     |           true                      |  boolean |

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
| ct            |      int            |     时间轴                      |  string   |
| did           |      string         |           true                      |  boolean |
| icon          |      string         |           true                      |  boolean |
| ip            |      string         |           true                      |  boolean |
| nick          |      string         |           true                      |  boolean |
| pg            |      int            |           true                      |  boolean |
| rg            |      int            |           true                      |  boolean |
| ts            |     long            |           true                      |  boolean |
| uid           |     int             |           true                      |  boolean |
| sts           |     long            |           true                      |  boolean |
| type          |     int             |           true                      |  boolean |
| room          |     string          |           true                      |  boolean |
