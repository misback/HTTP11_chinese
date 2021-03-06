报尾允许发送者在分块消息的最后包括额外的字段以提供可能在消息体被发送的时候被动态生成的元数据，例如消息的完整性检查，数字签名或者后期处理状态。除了报尾是在分块的尾部发送而不是在消息的头部分发送之外，报尾字段与头字段一样。

> ```
>   trailer-part   = *( header-field CRLF )
> ```

发送者**不得**生成一个包含下列情况所必须的字段的报尾：构成消息的必要字段（例如Transfer-Encoding和Content-Length），路由的必要字段（如Host），请求修饰符的必要字段（例如controls和条件语句，在RFC7231的第5节），认证的必要字段（例如，查看RFC7235和RFC6265），响应控制数据的必要字段（例如，查看RFC7231的7.1节），或者决定如何处理有效载荷的必要字段（例如，Content-Encoding，Content-Type，Content-Range和Trailer）。

当一个包含非空的报尾的分块消息被接收到的时候，接收者**可以**处理字段（除了上面禁止的字段），就好像他们被附加到消息的头部份一样。接收者**必须**忽略（或视作错误）任何在发送报文尾时禁止的字段，因为将他们视作在头部分出现的字段那样处理可能会绕过外部的安全过滤器。

除非请求中包含指示“报尾”的TE报头字段是可以接受的，否则服务器不应该生成它认为是用户代理接收所需的报尾字段。如果没有包含“报尾”的TE，服务器应该假设报尾字段可能会悄悄地丢弃到用户代理的路径上。 这个要求允许中介转发一个去分块的消息给HTTP / 1.0接收者而不缓冲整个响应。