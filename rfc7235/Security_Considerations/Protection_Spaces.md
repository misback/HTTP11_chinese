完全依赖“域”机制建立保护空间的验证方案会将证书暴露给原始服务器上的所有资源。已成功通过资源进行身份验证请求的客户端可以为同一个源服务器上的其他资源使用相同的身份验证凭据。这使得不同的资源可以获得其他资源的认证凭证。

当一个原始服务器在同一个规范的根URI（2.2节）下为多方提供资源时，这是特别关注的。可能的缓解策略包括限制对认证证书的直接访问（即，不使授权请求头部的内容可用），并且通过使用不同的主机名（或端口号）来为每一方分隔保护空间。