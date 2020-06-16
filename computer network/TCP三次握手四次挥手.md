### TCP三次握手
<details>
<summary>三次握手</summary>
  client将SYN置为1，随机产生一个初始序列号seq发送给Server,进入SYN_SENT状态</br>
  Server收到Client的SYN=1之后，知道客户端请求建立连接，将自己的SYN置1，ACK置1，产生一个acknowledge number=sequence number+1
并随机产生一个自己的初始序列号，发送给客户端，进入SYN_RCVD状态；</br>
  客户端检查acknodledge number是否为序列号+1，ACK是否为1检查正确之后将自己的ACK置1，产生一个acknowledge number = 服务器的序列号+1
发送给服务器，进入ESTABLISHED状态，服务器检查ACK为1和acknowledge number为序列号+1后，也进入ESTABLISHED状态；完成三次握手，连接建立</br>
</details>

<details>
<summary>为什么不能两次握手</summary>
  可能会出现已失效的连接请求报文段又传到了服务器端</br>
  client发出的第一个连接请求报文段并没有丢失，而是在某个网络节点长时间滞留了，以致延误到连接释放以后才到达server</br>
  server接收到延误的报文段后，发出确认保文段，但是client因为没有请求连接所以不会响应。server一直等待浪费很多资源</br>
  如果采用三次握手，server收不到确认，就知道client没有要求建立连接</br>
  server无法保证client收到确认报文<br/>
</details>

<details>
<summary>可以采用四次握手吗</summary>
  可以，但会降低传输效率
</details>

<details>
<summary>第三次握手中，客户端的ACK未送达服务器</summary>
  server:因为没有收到ACK确认，因此会重发之前的SYN+ACK（默认重发五次，之后自动关闭连接进入CLOSED状态）,client收到后会重新传ACK给server.</br>
  client:在server进行超时重发过程中，如果client向服务器发送数据,数据头部ACK是1，服务器收到数据后会读取ACK number，进入establish状态<br/>
  在server进入CLOSED状态后，如果client向服务器发送数据，服务器会以RST应答。
</details>

<details>
<summary>如果已经建立了连接，但客户端出现了故障怎么办</summary>
  服务器每收到一次客户端的请求后都会重新复位一个计时器，通常为2小时，超过则会每隔75s发送一次探测报文段，若超过10次，则关闭连接。
</details>

<details>
<summary>初始序列号是什么</summary>
  TCP连接的一方随机选择一个32位的序列号作为发送数据的初始序列号（ISN），以便接收方可以确认是否为合法编号。
</details>

### TCP四次挥手</br>
<details>
<summary>四次挥手</summary>
  Client将FIN置为1，发送一个序列号seq给Server,进入FIN_WAIT_1状态</br>
  Server收到FIN之后，发送一个ACK=1，acknowledge number=收到的序列号+1给服务器，进入CLOSED_WAIT状态，此时客户端已经没有要发送的数据了，但是仍然可以接收服务器发来的数据</br>
  Server将FIN置1，发送一个序列号给Client进入LAST_ACK状态</br>
  Client收到服务器的FIN后，进入TIME_WAIT状态，接着将ACK置一，发送一个acknowledge number=序列号+1给服务器；服务器收到后确认acknowledge number后变为CLOSED状态，不再向客户端发送数据。客户端等待2** MSL（保文段最长寿命）时间后，也进入CLOSED状态。完成四次挥手。</br>
  MSL(Maximum Segment Lifetime),指一个片段在网络中最大的存活时间，2MSL就是一个发送和一个回复所需的最大时间。如果直到2MSL，Client都没有再次收到FIN，那么Client推断ACK已经被成功接收
</details>

