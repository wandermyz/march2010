# 公钥算法 #
> 最近又跳出一个ECC，椭圆曲线算法。从资料中可以看出，ECC的资源消耗率很低，可以用很少的密钥长度和计算时间换来很高的安全性。因此这个是不是比RSA更有前景，更适合移动设备呢？

> 相关资料：
    * ECC vs RSA:
      * http://bbs.pediy.com/showthread.php?t=83431
      * http://chikaradirghsa.multiply.com/journal/item/16
    * ECC:(通俗易懂版)
      * http://tech.csai.cn/web/200604021704531906.htm
# OPENSSL #
  * OPENSSL开源（废话），貌似可以放手机上编译使用。不过没查到成功的例子，只查到一个尝试的例子：
> > http://www.forum.nokia.com/forum/showthread.php?t=93263
  * 另外PHP好像有对OPENSSL的支持：
> > http://www.php.net/manual/en/book.openssl.php
  * PENSSL有LIBRARY也有命令行工具，而且OPENSSL对ECC和RSA都是有实现的，因此掌握好OPENSSL基本上就掌握了加密算法。

# 待搞清楚的问题 #
  * 我们是否需要生成CERTIFICATE？啥用？有什么要求？
  * 服务器的认证：PKI（还是没搞清楚怎么才能防止别人伪装成我们的服务器）
  * HTTPS？(WANDER)

最后，一则8G（FROM 唐杰）

> NOKIA:
> > http://www.nokia.com.cn/find-products/happenings/innovationjourney