MIME要求互联网邮件主体部分在被转移前被转换为规范形式，如RFC2049第4节描述。本文档的3.1.1.3节描述了通过HTTP转移时，“文本”媒体类型的子类型允许的形式。RFC2046要求带有“文本”类型的内容用CRLF作为行终止符，并且禁止在换行符之外使用CR或LF。HTTP允许在文本内容中使用CRLF，CR和LF标识行终止。

从HTTP到严格MIME环境的代理或网关应该将本文档的3.1.1.3节中描述的文本媒体类型中的所有行中断都翻译为RFC2049的规范格式CRLF。但是注意，由于Content-Encoding的存在和HTTP允许一些不使用13和10表示CR和LF的字符集的事实，这可能是困难的。

转变将打破任何应用于原始内容的密码校验和，除非原始内容已经是规范形式。因此，规范形式对HTTP中使用这种校验和的任何内容都是推荐的。