# JSON Web Token

## 定义

- 本质上它是一段签名的 JSON 格式的数据

```
想象一下你刚从国外度完假回来，你在边境上说 - 你可以让我通过，我是这里的公民。这样的回答很好也没有问题，但是你要如何去支持你的说法呢？最有可能的方案是你携带了护照来证明你的身份。这里我们假设边境工作人员也都被要求去核实护照是真正由你的国家的护照办签发的。那么护照就会被核实，这样他们也才会放你回国。

现在，让我们从 JWT 的角度看一下这个故事，它们各自又都扮演着什么样的角色：

护照办 - 发布 JWT 的身份验证服务。

护照 - 你通过"护照办"获得的 JWT 签名。你的身份对于任何人都是可读的，但是只有它是真的时候相关方才会对其核实。

公民资格 - 在 JWT 中包含的你的声明（你的护照）。

边境 - 你的应用程序的安全层，在被允许访问受保护的资源之前由它来核实你的 JWT 令牌身份，在这种情况下指的是 - 国家。

国家 - 你想要获取的资源（例如 API）
```

## 没有session

简单来说，JWT 非常的酷，因为你不用再为了鉴别用户而在你的服务器上去保留你的 session 数据。这个工作流将会变得像下面这样：

- 用户调用身份验证服务，通常是发送了用户名及密码。
- 身份验证服务响应并返回了签名的 JWT，上面包含了用户是谁的内容。
- 用户向安全服务发送请求收到安全服务返回的令牌。
- 安全层检验令牌上的签名并且在签名为真的时候授权予以通过。

### 没有会话存储

### 没有对sessions的垃圾回收

### 真正的RESTful服务





### JWT 构成

- 头部： 关于签名算法的信息, 声明类型，那种JWT

  ```JSON
  {
    "typ": "JWT",
    "alg": "HS256"
  }
  ```

  ​

- 负载： json格式的实际数据

  ```json
  {
    "iss": "scotch.io", //发行商
    "exp": 1300819380, // 过期时间
    "name": "Chris Sevilleja", //其他信息
    "admin": true
  }
  ```

  ​

- 签名：

  - The third and final part of our JSON Web Token is going to be the signature. This signature is made up of a hash of the following components:

    - the header
    - the payload
    - secret

    ```json
    var encodedString = base64UrlEncode(header) + "." + base64UrlEncode(payload);

    HMACSHA256(encodedString, 'secret') = 

    03f329983b86f7d9a9f5fef85305880101d5e302afafa20154d094b229f75773
    ```

  ## 最终结果

  ```
  eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzY290Y2guaW8iLCJleHAiOjEzMDA4MTkzODAsIm5hbWUiOiJDaHJpcyBTZXZpbGxlamEiLCJhZG1pbiI6dHJ1ZX0.03f329983b86f7d9a9f5fef85305880101d5e302afafa20154d094b229f75773
  ```



## session 和 token

|      | session 和 token 就是个词而已…… 广义来说一切**维护用户状态**的技术都是session，一切动态生成的服务端有能力**鉴别真假**而本身无涵义的字符串都是token |
| ---- | ---------------------------------------- |
|      |                                          |