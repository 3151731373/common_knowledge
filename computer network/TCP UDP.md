### TCP三次握手，四次挥手
第一次握手：client将SYN置为1，随机产生一个初始序列号seq发送给Server,进入SYN_SENT状态</br>
第二次握手：Server收到Client的SYN=1之后，知道客户端请求建立连接，将自己的SYN置1，ACK置1，产生一个acknowledge number=sequence number+1
并随机产生一个自己的初始序列号，发送给客户端，进入SYN_RCVD状态；</br>
第三次握手：客户端检查acknodledge number是否为序列号+1，ACK是否为1检查正确之后将自己的ACK置1，产生一个acknowledge number = 服务器的序列号+1
发送给服务器，进入ESTABLISHED状态，服务器检查ACK为1和acknowledge number为序列号+1后，也进入ESTABLISHED状态；完成三次握手，连接建立</br>


### TCP与UDP的区别

1. TCP是面向连接的，UDP是无连接的；
<details>
<summary>什么叫无连接</summary>

UDP发送数据之前不需要建立连接
</details>

2.TCP是可靠的，UDP是不可靠的
<details>
  <summary>什么是不可靠</summary>
  UDP接收到报文后，不需要给出任何确认
</details>

3.TCP只支持点对点通信，UDP支持一对一，一对多，多对一，多对多

4.TCP是面向字节流的，UDP是面向报文的
<details>
  <summary>什么意思</summary>
  面向字节流是指发送数据时以字节为单位，一个数据包可以拆分成若干组进行发送，而UDP一个报文只能一次发完。
</details>

5.TCP有拥塞控制机制，UDP没有。网络出现的拥塞不会使源主机的发送速率降低，这对某些实时应用是很重要的，比如媒体通信，游戏

6.TCP首部开销20字节，UDP首部开销8字节

7.UDP的主机不需要维持复杂的连接状态表
