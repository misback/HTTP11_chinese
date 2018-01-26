#### must-revalidate

“must-revalidate”响应指令表明一旦响应过期，缓存**不得**在没有从源站成功校验的情况下使用这个响应来满足后续请求。

must-revalidate指令对于某些协议特性的可靠运行支持是必要的。在所有情况中缓存都**必须**遵守must-revalidate指令；特别的，如果一个缓存出于任何原因不能叨叨源服务器，它**必须**生成要给504响应。

当且仅当对一个表示的请求校验失败可能导致不正确的运行时，must-revalidate指令应该被服务器使用，例如一个默认未执行的金融交易。

#### no-cache

参数语法：

> ```
>       #field-name
> ```

“no-cache”响应指令表明响应在没有成功从源服务器校验的时候**不得**被用来满足一个后续请求。这使得源服务器能够阻止一个缓存在未与它取得联系的时候使用缓存来满足一个请求，即使通过配置为发送陈旧响应的缓存也是如此。

如果no-cache响应指令指定了一个或多个字段名，那么缓存**可以**使用那个响应来满足后续请求，受制于任何其他缓存限制。但是，任何带有列出字段名的响应中的头字段**不得**在未与源服务器成功校验的时候在后续请求的响应中发送。这使得源服务器能阻止具体头字段在响应中的复用，并且继续允许缓存响应的剩余部分。

给出的字段名不限制于本协议定义的头字段。字段名是不区分大小写的。

这个使用使用参数语法的双引号字符串形式。发送者**不应该**生成标记形式（即使对于单个条目的列表引号明显是不必要的）。

*注意：虽然它已经被移植到很多实现中，单一些HTTP/1.0的缓存会无法识别或遵守这个指令。此外，带有字段名称的no-cache响应指令通常由高速缓存处理，就像接收到非限定的no-cache指令一样;即，对于合格形式的特别处理并没有被广泛实现。*

#### no-store

“no-store”响应指令表明缓存**不得**存储及时请求或响应的任何部分。这个指令适用于私有和共享缓存。“**不得**存储”在这个上下文的意思是缓存**不得**故意将信息存储到非易失性存储，并**必须**尽最大努力尝试在转发消息后将信息尽快从易失性存储中删除。

这个指令**不是**一个可靠或足够的机制来保证隐私。特别的，恶意的或受损的缓存可能不会识别或遵守这个指令，并且通讯网络很容易遭到窃听。

#### no-transform

“no-transform”响应指令表示一个中介（无论它是否实现了一个缓存）**不得**转化负载，如RFC7230，5.7.2节定义。

#### public

“public”响应指令表明任何缓存**可以**存储这个响应，即使响应通常是不可缓存的或只可以在私有缓存中缓存。（查看3.2节了解关于包含Authorization请求的响应中public使用的额外细节，以及第3节的public如何影响由于状态码的定义默认不可缓存的那些通常不被缓存的响应的细节；查看4.2.2节）

#### private

参数语法：

> ```
>       #field-name
> ```

“private”响应指令表明响应消息是打算给单个用户的，并且**不得**被共享缓存存储。一个私有缓存**可以**存储这个响应并为之后的请求使用它，即使这个响应通常是不可缓存的。

如果private响应指令指定了一个或多个字段名，这个要求被限制到与列出的字段值相关的响应头字段。即，共享缓存**不得**存储特定的字段名，而它可以存储响应消息的剩余部分。

给出的字段名不限于本规范定义的头字段集合。字段名是不区分大小写的。

这个指令使用参数语法的双引号字符串形式。一个发送者**不应该**生成标记形式（即使对于单个条目的列表引号明显是不必要的）。

*注意：“private”的使用只控制了响应可以被存储；它不能保证消息内容的私密性。带有字段名的private响应指令通常由缓存处理，就像接收到非限定的private指令一样；即，对于合格形式的具体处理并没有被广泛实现。*

#### proxy-revalidate

“proxy-revalidate”响应指令与must-revalidate有相同的含义，除了它不适用于私有缓存。

#### max-age

参数语法：

> ```
>       delta-seconds (see Section 1.2.1)
> ```

“max-age”响应指令表明在它的年龄比指定的秒数大以后它将被视为过期的。

这个指令使用参数语法的标记形式：例如，`max-age=5`而不是`max-age="5"`。发送者**不应该**生成双引号字符串形式。

#### s-maxage

参数语法：

> ```
>       delta-seconds (see Section 1.2.1)
> ```

”s-maxage“响应指令表明在共享缓存中由这个指令指定的最大年龄覆盖由max-age指令或Expires头字段指定的最大年龄。s-maxage指令也暗示了proxy-revalidate响应指令的语义。

这个指令使用参数语法的标记形式：例如，`s-maxage=10`而不是`smaxage="10"`。发送者**不应该**生成双引号字符串形式。