两个头字段被用于携带认证凭证，如RFC7235中定义。请注意，用于用户身份验证的各种自定义机制为此使用Cookie标头字段，如RFC6265中所定义。

> ```
>    +---------------------+--------------------------+
>    | Header Field Name   | Defined in...            |
>    +---------------------+--------------------------+
>    | Authorization       | Section 4.2 of [RFC7235] |
>    | Proxy-Authorization | Section 4.4 of [RFC7235] |
>    +---------------------+--------------------------+
> ```

