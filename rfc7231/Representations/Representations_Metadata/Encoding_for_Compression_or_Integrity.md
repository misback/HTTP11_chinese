#### 内容编码

内容编码的值指明已经被用于或可以被用于一个表示的编码转换。内容编码主要被用于表示的压缩或者其他不丢失底层媒体类型的识别和信息的转换。多数情况，表示以编码的形式存储，直接发送，并且只被最终的接收者解码。

> ```
>   content-coding   = token
> ```

所有的content-coding值是不区分大小写的并且应该被注册在“HTTP内容编码注册表”中，如8.4节定义。他们被用于Accept-Encoding（5.3.4节）和Content-Encoding（3.1.2.2节）头字段中。

下面的几个content-coding值由本规范定义：
>       compress (and x-compress): See Section 4.2.1 of [RFC7230].
>       
>       deflate: See Section 4.2.2 of [RFC7230].
>       
>       gzip (and x-gzip): See Section 4.2.3 of [RFC7230].

#### Content-Encoding

“Content-Encoding”头字段表明已经除了那些媒体类型固有的编码外，已经被应用到表示的内容编码，以及因此为了获得由“Content-Type”头字段引用的媒体类型中的数据必须应用的解码机制。Content-Encoding主要被用于允许表示的数据被压缩而不丢失底层媒体类型的识别。

> ```
>     Content-Encoding = 1#content-coding
> ```

下面是它的用法的一个例子：
> ```
>     Content-Encoding: gzip
> ```

如果一个多多个编码被用于表示，应用编码的发送者必须**生成**一个Content-Encoding投资段，其以它们被应用的顺序列出了内容编码。关于编码参数的额外信息可以由其他头字段提供，他们没有在本规范中定义。

与传输编码（RFC7230，3.3.1节）不同，Content-Encoding中列出的编码是表示的特性，表示以编码形式来定义，除非在元数据定义中另有说明，否则关于表示的所有其他元数据是关于编码形式的。典型地，该表示仅在渲染或类似使用之前被解码。

如果媒体类型包含了一个固有的编码，例如一个压缩的数据格式，那么那个编码将不会被重复呈现在Content-Encoding中，解释它碰巧与内容编码的其中一个逻辑相同。这样的内容编码只可能出于一些异常原因被列出，如果如果它被两次用于格式表示。同样的，源服务器可能选择以多种表示发布一个相同的数据，他们仅在编码被定义为Content-Type或Content-Encoding的一部分方面有所不同，因为一些用户代理在处理每个响应时有不同的行为（例如，打开“另存为”对话框而不是解压缩并解读内容）。

如果请求消息中的表示有一个不可接受的内容编码，源服务器**可能**以一个415状态码（不支持的媒体类型）来响应。