# bootstrapping

Bootstrapping 有以下两种类型：

- 一种是用于客户端的Bootstrap
- 一种是用于服务端的ServerBootstrap

| 分类                | Bootstrap            | ServerBootstrap |
| ------------------- | -------------------- | --------------- |
| 网络功能            | 连接到远程主机和端口 | 绑定本地端口    |
| EventLoopGroup 数量 | 1                    | 2               |

“ServerBootstrap”监听在服务器监听一个端口轮询客户端的“Bootstrap”或DatagramChannel是否连接服务器。通常需要调用“Bootstrap”类的connect()方法，但是也可以先调用bind()再调用connect()进行连接，之后使用的Channel包含在bind()返回的ChannelFuture中。



一个 ServerBootstrap 可以认为有2个 Channel 集合，第一个集合包含一个单例 ServerChannel，代表持有一个绑定了本地端口的 socket；第二个集合包含所有创建的 Channel，处理服务器所接收到的客户端进来的连接。下图形象的描述了这种情况：

![Figure%203](assets/1502159260674064.jpg)

与 ServerChannel 相关 EventLoopGroup 分配一个 EventLoop 是 负责创建 Channels 用于传入的连接请求。一旦连接接受，第二个EventLoopGroup 分配一个 EventLoop 给它的 Channel。



