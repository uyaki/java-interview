# 认识Netty的ChannelHandler 和 ChannelPipeline

![Figure%203](assets/1502159325575539.jpg)

进站和出站的处理器都可以被安装在相同的 pipeline

*在当前的链（chain）中，事件可以通过 ChanneHandlerContext 传递给下一个 handler。Netty 为此提供了抽象基类ChannelInboundHandlerAdapter 和 hannelOutboundHandlerAdapter，用来处理你想要的事件。*

在 Netty 发送消息可以采用两种方式：

- 直接写消息给 Channel 

- 写入 ChannelHandlerContext 对象。


> 这两者主要的区别是， 前一种方法会导致消息从 ChannelPipeline的尾部开始，而后者导致消息从 ChannelPipeline 下一个处理器开始。

