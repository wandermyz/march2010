对所有发送到手机端的请求，格式如下：

> Content-Type为application/octet-stream

> 内容：

> 先给一个二进制串（假设所有正常请求不会以这样的字符串开头）
```
  00 FF 00 FF 00 FF FF FF
```
> 紧接着是服务器公告的base64编码（ASCII编码，没有加urlencode）