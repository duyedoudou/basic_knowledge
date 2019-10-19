### https加密

#### http：

明文传输。

#### 对称加密：

服务器先生成一把**密钥**，然后先把密钥传输给客户端。之后服务器给客户端发送真实数据的时候，会用这把密钥对数据进行加密，客户端收到加密数据之后，用刚才收到的密钥进行解密。

![img](https://mmbiz.qpic.cn/mmbiz_png/gsQM61GSzINicVDniaGT5Y5wgjBOUrJlGAwk1YvjOgSJTvQjrgLUVDSlTYJLzFa9SKg0kQOJbEP9ly48JtPrNiatA/640?)

问题：服务器是通过**明文传输密钥**的，所以喽，如果秘钥被中间人捕获，那就和明文没区别了。

#### 非对称加密：

服务器和客户端都拥有2把密钥（公钥和私钥），**用公钥加密的数据只有对应的私钥才能打开，用私钥加密的数据只有公钥才能打开。**重点奥

![img](https://mmbiz.qpic.cn/mmbiz_png/gsQM61GSzINicVDniaGT5Y5wgjBOUrJlGAb3dmof8RxGton6vNIxzgeQEIR66AF03csULiaPr81oN0w2erbjRAqxQ/640?)

问题：非对称加密特别慢！

优化：用非对称加密的方式来传输对称加密的密钥。服务器用明文将自己的公钥（公蛋蛋）用明文发给客户端，客户端把`对称加密将用的密钥`用公蛋蛋加密，发回给服务器。（此处以一端为例子）

问题：但是中间人可以截获公蛋蛋，并换成自己的公蛋蛋！

![image-20191019185422721](/Users/mac/Library/Application Support/typora-user-images/image-20191019185422721.png)

原因：非对称加密之所以不安全，是因为客户端不知道那个公蛋蛋不是服务器的。

那么，就需要找到一种策略来证明这把公钥就是服务器的，而不是别人冒充的。

#### 数字证书：

服务器在给客户端传输公蛋蛋的过程中，会把公蛋蛋以及服务器的个人信息通过Hash算法生成信息摘要。

![image-20191019185735375](/Users/mac/Library/Application Support/typora-user-images/image-20191019185735375.png)



为了防止信息摘要被人调换，服务器还会用`认证中心`提供的私钥对信息摘要进行加密来形成数字签名。

![image-20191019185916515](/Users/mac/Library/Application Support/typora-user-images/image-20191019185916515.png)

最后把好几个信息打包，形成数字证书。

![image-20191019190003768](/Users/mac/Library/Application Support/typora-user-images/image-20191019190003768.png)

客户端拿到这份数字证书之后，用认证中心提供的公钥来对数字证书里面的数字签名进行解密来得到信息摘要1；

然后对数字证书里服务器的公钥以及个人信息进行Hash得到另外一份信息摘要2。

最后把两份信息摘要进行对比，如果一样，则证明这个人是服务器，否则就不是。

来源：https://mp.weixin.qq.com/s?__biz=MzIwNTc4NTEwOQ==&mid=2247486036&idx=1&sn=dd3f322e0960b813bc8fc17542fd800e&scene=21#wechat_redirect

