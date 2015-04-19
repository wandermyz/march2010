# 服务器端以及通信协议 #
## 支持单操作获取全部更新 ##
  * 只发自己的Encrypted Index(512BYTE)上来，由硬件生成所有CONNECTION的INDEX，然后自动增量更新，并记录自己的最后更新时间。这个主要是为了减少更新的流量，现在流量太大。
## 在传输的包前加一个包头 ##
  * 带上版本号，长度之类的，这样的话可以支持传输变长数据，进一步减少流量，增大灵活性。版本号可以使得多版本的用户数据一起传输，这样可以有利于以后对于用户的数据做分类，或者提供VIP区别之类的。
# Android #
## 用户数据多样化 ##
  * 虽然我们网络传输的时候还是传输一个string，但是我们可以在客户端进行解析，识别出电子邮箱、QQ号、地址、地点、活动、心情……这样的话我们就牛了呀！
# S60 #
# WEB/WAP #
## 增加自动的投票、排名系统 ##
  * 比如对于外卖的每一个菜单进行投票……