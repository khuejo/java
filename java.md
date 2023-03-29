# 序列化
## 序列化与反序列化是什么？
互联网的产生带来了机器间通讯的需求，而互联通讯的双方需要采用约定的协议，序列化和反序列化属于通讯协议的一部分。
通讯协议往往采用分层模型，不同模型每层的功能定义以及颗粒度不同，例如：TCP/IP协议是一个四层协议，而OSI模型却是七层协议模型。
在OSI七层协议模型中展现层（Presentation Layer）的主要功能是把应用层的对象转换成一段连续的二进制串，或者反过来，把二进制串转换成应用层的对象–这两个功能就是序列化和反序列化。
一般而言，TCP/IP协议的应用层对应与OSI七层协议模型的应用层，展示层和会话层，所以序列化协议属于TCP/IP协议应用层的一部分。本文对序列化协议的讲解主要基于OSI七层协议模型。
- 序列化： 将数据结构或对象转换成二进制串的过程
- 反序列化：将在序列化过程中所生成的二进制串转换成数据结构或者对象的过程

## 有哪些常见的序列化协议？
- JSON：一种轻量级的数据交换格式，以键值对的形式表示数据，易于阅读和编写，并且支持跨语言使用。
```json
{
    "name": "John",
    "age": 30,
    "isMarried": true,
    "hobbies": [
        "reading",
        "traveling",
        "swimming"
    ],
    "address": {
        "street": "123 Main Street",
        "city": "New York",
        "state": "NY",
        "zipCode": "10001"
    }
}
```

- XML：一种基于文本的标记语言，具有良好的可扩展性和互操作性，但相比于JSON等格式较为冗长。
```xml
<?xml version="1.0" encoding="UTF-8"?>
<bookstore>
  <book category="cooking">
    <title lang="en">The Joy of Cooking</title>
    <author>Irma S. Rombauer</author>
    <year>1931</year>
    <price>25.99</price>
  </book>
  <book category="children">
    <title lang="en">Harry Potter and the Philosopher's Stone</title>
    <author>J.K. Rowling</author>
    <year>1997</year>
    <price>19.99</price>
  </book>
</bookstore>
```

- Thrift：由Facebook开发的高效的跨语言序列化框架，支持多种数据格式和传输协议，适用于大型分布式系统中的数据交换。
```thrift
binary protocol
struct User {
  1: string name,
  2: i32 age
}

// 请求消息格式
struct GetUserRequest {
  1: i64 userId   // 用户ID
}

// 响应消息格式
struct GetUserResponse {
  1: User user   // 用户信息
}

// Thrift服务定义
service UserService {
  GetUserResponse getUser(1: GetUserRequest request)
}
```

- Protobuf：由Google开发的高性能序列化框架，采用二进制编码，具有卓越的解析速度和空间利用率，常用于高并发场景中。
```protobuf
syntax = "proto3";
package mypackage;

message User {
  string name = 1;
  int32 age = 2;
}

// 请求消息格式
message GetUserRequest {
  int64 user_id = 1;   // 用户ID
}

// 响应消息格式
message GetUserResponse {
  User user = 1;   // 用户信息
}
```

- Avro：一种基于二进制的数据序列化框架，支持跨语言和版本控制，具有很好的兼容性和可扩展性。
```avro

```

- MessagePack：一种基于二进制的高性能序列化格式，支持多种编程语言，可以实现快速的数据序列化和反序列化。

总之，不同的序列化协议各有特点，开发人员可以根据实际需求和应用场景选择合适的协议，以便在不同的系统之间进行数据交换或持久化操作

参考：[序列化和反序列化-美团](https://tech.meituan.com/2015/02/26/serialization-vs-deserialization.html)
