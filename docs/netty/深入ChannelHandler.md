# 深入ChannelHandler

## 编码器、解码器

当您发送或接收消息时，Netty 数据转换就发生了。入站消息将从字节转为一个Java对象;也就是说，“解码”。如果该消息是出站相反会发生：“编码”，从一个Java对象转为字节。其原因是简单的：网络数据是一系列字节，因此需要从那类型进行转换。



在一般情况下，基类将有一个名字类似` ByteToMessageDecoder` 或 `MessageToByteEncoder`。在一种特殊类型的情况下，你可能会发现类似 ProtobufEncoder 和 ProtobufDecoder，用于支持谷歌的 protocol buffer。



严格地说，其他处理器可以做编码器和解码器能做的事。但正如适配器类简化创建通道处理器，**所有的编码器/解码器适配器类都实现自 ChannelInboundHandler 或 ChannelOutboundHandler**。



对于入站数据，**channelRead 方法/事件被覆盖**。这种方法在每个消息从入站 Channel 读入时调用。该方法将调用特定解码器的“解码”方法，并将解码后的消息转发到管道中下个的 ChannelInboundHandler。

出站消息是类似的。编码器将消息转为字节，转发到下个的 ChannelOutboundHandler。

## SimpleChannelHandler

也许最常见的处理器是接收到解码后的消息并应用一些业务逻辑到这些数据。

要创建这样一个 ChannelHandler，你只需要扩展基类`SimpleChannelInboundHandler<T>` 其中 T 是想要进行处理的类型。

在这种类型的处理器方法中的最重要是 channelRead0(ChannelHandlerContext，T)。在这个调用中，T 是将要处理的消息。 你怎么做，完全取决于你，但无论如何你不能阻塞 I/O线程，因为这可能是不利于高性能。



## 阻塞操作

*I/O 线程一定不能完全阻塞，因此禁止任何直接阻塞操作在你的 ChannelHandler， 有一种方法来实现这一要求。你可以指定一个 EventExecutorGroup。当添加 ChannelHandler 到ChannelPipeline。此 EventExecutorGroup 将用于获得EventExecutor，将执行所有的 ChannelHandler 的方法。这EventExecutor 将从 I/O 线程使用不同的线程，从而释放EventLoop。*

