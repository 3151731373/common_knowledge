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


<details>
<summary></summary>
</details>
