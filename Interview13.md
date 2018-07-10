# 计算机网络面试问题集锦  

## TCP的三次握手四次挥手
  
### 建立连接协议（三次握手）
  
* 1. 客户端发送一个带SYN标志的TCP报文到服务器。这是三次握手过程中的报文1。
* 2. 服务器端回应客户端的，这是三次握手中的第2个报文，这个报文同时带ACK标志和SYN标志。因此它表示对刚才客户端SYN报文的回应；同时又标志SYN给客户端，询问客户端是否准备好进行数据通讯。
* 3. 客户必须再次回应服务段一个ACK报文，这是报文段3   

![icon](img/Interview13-img01.png)    
   
### 连接终止协议（四次挥手）    
   
>由于TCP连接是全双工的，因此每个方向都必须单独进行关闭。这原则是当一方完成它的数据发送任务后就能发送一个FIN来终止这个方向的连接。收到一个 FIN只意味着这一方向上没有数据流动，一个TCP连接在收到一个FIN后仍能发送数据。首先进行关闭的一方将执行主动关闭，而另一方执行被动关闭。    


（1） TCP客户端发送一个FIN，用来关闭客户到服务器的数据传送（报文段4）。   
（2） 服务器收到这个FIN，它发回一个ACK，确认序号为收到的序号加1（报文段5）。和SYN一样，一个FIN将占用一个序号。    
（3） 服务器关闭客户端的连接，发送一个FIN给客户端（报文段6）。   
（4） 客户段发回ACK报文确认，并将确认序号设置为收到序号加1（报文段7）。    
    
  
![icon](img/Interview13-img02.png)      
     

   
### 6. TCP和UDP的区别？

TCP提供面向连接的、可靠的数据流传输，而UDP提供的是非面向连接的、不可靠的数据流传输。

TCP传输单位称为TCP报文段，UDP传输单位称为用户数据报。

TCP注重数据安全性，UDP数据传输快，因为不需要连接等待，少了许多操作，但是其安全性却一般。    
   
  
![icon](img/Interview13-img04.png)    
   
  
![icon](img/Interview13-img05.png)    
   
### 7. Http和Https的区别

Http协议运行在TCP之上，明文传输，客户端与服务器端都无法验证对方的身份；Https是身披SSL(Secure Socket Layer)外壳的Http，运行于SSL上，SSL运行于TCP之上，是添加了加密和认证机制的HTTP。二者之间存在如下不同：

端口不同：Http与Http使用不同的连接方式，用的端口也不一样，前者是80，后者是443；

资源消耗：和HTTP通信相比，Https通信会由于加减密处理消耗更多的CPU和内存资源；

开销：Https通信需要证书，而证书一般需要向认证机构购买； 
　 
Https的加密机制是一种共享密钥加密和公开密钥加密并用的混合加密机制。   
   
  
### 8. 对称加密与非对称加密

对称密钥加密是指加密和解密使用同一个密钥的方式，这种方式存在的最大问题就是密钥发送问题，即如何安全地将密钥发给对方；而非对称加密是指使用一对非对称密钥，即公钥和私钥，公钥可以随意发布，但私钥只有自己知道。发送密文的一方使用对方的公钥进行加密处理，对方接收到加密信息后，使用自己的私钥进行解密。

由于非对称加密的方式不需要发送用来解密的私钥，所以可以保证安全性；但是和对称加密比起来，它非常的慢，所以我们还是要用对称加密来传送消息，但对称加密所使用的密钥我们可以通过非对称加密的方式发送出去。
   
   
### 9. 为什么TCP链接需要三次握手，两次不可以么，为什么？

为了防止 已失效的链接请求报文突然又传送到了服务端，因而产生错误。

客户端发出的连接请求报文并未丢失，而是在某个网络节点长时间滞留了，以致延误到链接释放以后的某个时间才到达Server。这是，Server误以为这是Client发出的一个新的链接请求，于是就向客户端发送确认数据包，同意建立链接。若不采用“三次握手”，那么只要Server发出确认数据包，新的链接就建立了。由于client此时并未发出建立链接的请求，所以其不会理睬Server的确认，也不与Server通信；而这时Server一直在等待Client的请求，这样Server就白白浪费了一定的资源。若采用“三次握手”，在这种情况下，由于Server端没有收到来自客户端的确认，则就会知道Client并没有要求建立请求，就不会建立链接。    
   
  
![icon](img/Interview13-img06.png)    
   
  
![icon](img/Interview13-img07.png)   
   
  
![icon](img/Interview13-img08.png)   
   
   
![icon](img/Interview13-img09.png)    
   
  
![icon](img/Interview13-img10.png)    
   
  
![icon](img/Interview13-img11.png)    
   
  
![icon](img/Interview13-img12.png)    
   
   
![icon](img/Interview13-img13.png)    
  
   
![icon](img/Interview13-img14.png)    
   
   
![icon](img/Interview13-img15.png)     
   
  
![icon](img/Interview13-img16.png)    
   
   
![icon](img/Interview13-img17.png)   
   
  
![icon](img/Interview13-img18.png)   
   
  
![icon](img/Interview13-img19.png)   
   
  
![icon](img/Interview13-img20.png)   
   
  
![icon](img/Interview13-img21.png)   
   
  
![icon](img/Interview13-img22.png)  
   
  
![icon](img/Interview13-img23.png) 
   
  
![icon](img/Interview13-img24.png) 
   
  
![icon](img/Interview13-img25.png) 
   
  
![icon](img/Interview13-img26.png)   
