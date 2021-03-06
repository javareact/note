##  [密码学的基本分类](http://blog.csdn.net/LonelyRoamer/article/details/7630594)
* 密码学在加密算法上大体可分为单向加密算法、对称加密算法、非对称加密算法。
* 单向加密算法: 散列函数广泛用于信息完整性的验证，是数据签名的核心技术，散列函数的常用算法有MD----消息摘要算法、SHA-----安全散列算法及MAC-----消息认证码算法。
* DES是典型的对称加密算法的代表，对称加密算法是数据存储加密的常用算法。
* 对称密码体制分为两种：一种是对明文的单个位（或字节）进行运算，称为流加密，也称序列加密。另一种是把明文信息划分成不同的组（或块）结构，分别对每个组（或块）进行加密和解密，称为分组加密（例如：DES）。
* RSA算法是非对称加密算法的代表，非对称加密算法是数据传输加密的常用算法。
* 在非对称密码体制中，公钥和私钥均可用于加密和解密操作，但它与对称密码体制不同。公钥与私钥分属通信双方，一份消息的加密和解密需要公钥与私钥共同参与。公钥加密则需要私钥解密，反之，私钥加密则需要公钥解密。
## The Public-Key Cryptography Standards (PKCS)[PKCS 发布的15 个标准](http://falchion.iteye.com/blog/1472453)
* 是由 RSA 实验室与其它安全系统开发商为促进公钥密码的发展而制订的一系列标准。
##  [Base64算法](http://blog.csdn.net/LonelyRoamer/article/details/7633183)
## [消息摘要算法简介](http://blog.csdn.net/LonelyRoamer/article/details/7638478)
## 加密技术包括两个元素：算法和密钥
## java 中 Security.getProviders() 返回结果：
* 每个 provider 有一个名称和一个版本号，并且在每个它装入运行时中进行配置。  
* `[SUN version 1.7, SunRsaSign version 1.7, SunEC version 1.7, SunJSSE version 1.7, SunJCE version 1.7, SunJGSS version 1.7, SunSASL version 1.7, XMLDSig version 1.0, SunPCSC version 1.7, SunMSCAPI version 1.7]`
## jdk 默认的 强加密随机数生成器类 使用的算法
`new SecureRandom().getAlgorithm()`  
`new SecureRandom().getProvider()`  
`SHA1PRNG`  // 算法  
`SUN version 1.7` // 提供者
## [理解AES加密解密的使用方法](http://blog.csdn.net/vieri_32/article/details/48345023)
## Diffie-Hellman密钥交换算法 [廖雪峰](https://zhuanlan.zhihu.com/p/21513964)
> 首先，小明先选一个素数和一个底数，例如，素数p=23，底数g=5（底数可以任选），再选择一个秘密整数a=6，计算A=g^a mod p=8，然后传纸条给女神：p=23，g=5，A=8；  
> 女神收到纸条后，也选一个秘密整数b=15，然后计算B=g^b mod p=19，并传纸条告诉小明：B=19；  
> 小明自己计算出密码s=B^a mod p=2，女神也自己计算出密码s=A^b mod p=2，因此，小明和女神最终协商的密码s为2。  
> 而这一切都发生在老王的眼皮底下，他却无法计算出小明和女神协商的密码：
## 对称加密与非对称加密 [原创](http://www.cnblogs.com/jfzhu/p/4020928.html)
（1） 对称加密加密与解密使用的是同样的密钥，所以速度快，但由于需要将密钥在网络传输，所以安全性不高。（选择了Rijndael算法作为新的高级加密标准（AES--Advanced Encryption Standard））

（2） 非对称加密使用了一对密钥，公钥与私钥，所以安全性高，但加密与解密速度慢。（非对称加密算法是RSA算法，是Rivest, Shamir, 和Adleman于1978年发明）

（3） 解决的办法是将对称加密的密钥使用非对称加密的公钥进行加密，然后发送出去，接收方使用私钥进行解密得到对称加密的密钥，然后双方可以使用对称加密来进行沟通。

## HTTPS
[https by 腾讯Bugly](https://mp.weixin.qq.com/s?__biz=MzA3NTYzODYzMg==&mid=402615812&idx=1&sn=b6dae639119bb66e7025321254b8d973&scene=1&srcid=122439MA3l7gRwfjgNOB76pA#rd)
## 数字证书文件格式（cer和pfx）的区别 [转载](http://blog.csdn.net/wangjun_pfc/article/details/5493900)
* 作为文件形式存在的证书一般有这几种格式：   
1. 带有私钥的证书  
　　由Public Key Cryptography Standards #12，PKCS#12标准定义，包含了公钥和私钥的二进制格式的证书形式，以pfx作为证书文件后缀名。  
2. 二进制编码的证书  
证书中没有私钥，扩展名DER用于二进制DER编码的证书。这些证书也可以用CER或者CRT作为扩展名。比较合适的说法是“我有一个DER编码的证书”，而不是“我有一个DER证书”。
3. Base64编码的证书  
证书中没有私钥，BASE64 编码格式的证书文件（各种X.509 v3 证书），也是以cer作为证书文件后缀名。  

* 由定义可以看出，只有pfx格式的数字证书是包含有私钥的，cer格式的数字证书里面只有公钥没有私钥。
 
* 在pfx证书的导入过程中有一项是“标志此密钥是可导出的。这将您在稍候备份或传输密钥”。一般是不选中的，如果选中，别人就有机会备份你的密钥了。如果是不选中，其实密钥也导入了，只是不能再次被导出。这就保证了密钥的安全。
* 如果导入过程中没有选中这一项，做证书备份时“导出私钥”这一项是灰色的，不能选。只能导出cer格式的公钥。如果导入时选中该项，则在导出时“导出私钥”这一项就是可选的。
* 如果要导出（pfx)私钥,是需要输入密码的，这个密码就是对私钥再次加密，这样就保证了私钥的安全，别人即使拿到了你的证书备份（pfx),不知道加密私钥的密码，也是无法导入证书的。相反，如果只是导入导出cer格式的证书，是不会提示你输入密码的。因为公钥一般来说是对外公开的，不用加密
* der类型的不用在编码解码，直接就是二进制的数据可以直接使用；
* pem类型的数据要根据base64编码解码后，得到的数据需要进行增加或裁剪特殊字符-、\n、\r、begin信息、end信息等。
## 证书文件格式标准 [转载](http://blog.csdn.net/xiao_zhu_kuai_pao/article/details/45675509)
* PEM是OpenSSL和许多其他SSL工具的标准格式，OpenSSL 使用PEM 文件格式存储证书和密钥。这种格式被设计用来安全的包含在ascii甚至富文本文档中，如电子邮件。这意味着您可以简单的复制和粘贴pem文件的内容到另一个文档中。
* PEM文件是Base64编码的证书。PEM证书通常用于web服务器，因为他们可以通过一个简单的文本编辑器，很容易地转换成可读的数据。通常当一个PEM编码在文本编辑器中打开文件,它会包含不同的页眉和页脚。：

1. CSR(证书签名请求)  
-----BEGIN CERTIFICATE REQUEST-----   
xxx   
-----END CERTIFICATEREQUEST-----    

2. 私钥   
-----BEGIN RSA PRIVATE KEY-----  
xxx   
-----END RSA PRIVATEKEY-----  

3. 证书文件  
-----BEGIN CERTIFICATE-----  
 xxx  
-----END CERTIFICATE-----  
4. PKCS #8: Private-Key Information Syntax（语法） Standard（标准）


## [openssl](https://baike.baidu.com/item/openssl/5454803?fr=aladdin)
* OpenSSL：是一个强大的安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理功能及SSL协议，并提供丰富的应用程序供测试或其它目的使用。
* OpenSSL整个软件包大概可以分成三个主要的功能部分：密码算法库、SSL协议库以及应用程序。OpenSSL的目录结构自然也是围绕这三个功能部分进行规划的。
### centos6 升级 openssl 详解
#### 1 编译安装
* 下载最新 `wget https://www.openssl.org/source/openssl-1.0.2-latest.tar.gz`
* 解压 `tar xzvf openssl-1.0.2n.tar.gz` ,并进入解压后的目录
* 执行文件夹中的config文件，这里openssl的安装目录默认是/usr/local/ssl（由于系统环境差异路径可能不一致，下同），注意添加zlib-dynamic参数，使其编译成动态库  
`./config shared zlib-dynamic`  
`make`  
`make install`  
#### 2 更新相关执行文件、库文件 
* 重命名原来的openssl命令
`mv /usr/bin/openssl  /usr/bin/openssl.old`
* 重命名原来的openssl目录
`mv /usr/include/openssl  /usr/include/openssl.old`
* 将安装好的openssl 的openssl命令软连到/usr/bin/openssl
`ln -s /usr/local/ssl/bin/openssl  /usr/bin/openssl`
* 将安装好的openssl 的openssl目录软连到/usr/include/openssl
`ln -s /usr/local/ssl/include/openssl  /usr/include/openssl`

* 修改系统自带的openssl库文件。可以看到：  
Centos6.5 的是在/usr/lib/libssl.so  和/usr/lib/libssl.so.1.0.1
其中/usr/lib/libssl.so是/usr/lib/libssl.so.1.0.1的软连接
只需要把/usr/local/ssl/lib/libssl.so.1.0.0替换为/usr/lib/libssl.so.1.0.1即可。  
`mv /usr/lib/libssl.so.1.0.0  /usr/lib/libssl_so.1.0.0_bak`  
`cp  /usr/local/ssl/lib/libssl.so.1.0.0  /usr/lib/libssl.so.1.0.0`  
* 同样，更新 /usr/lib64/libcrypto.so.1.0.0 为新的/usr/local/ssl/lib/libcrypto.so.1.0.0 库文件
* 检查是否操作正确
执行命令查看openssl依赖库版本是否为1.0.2n：
`strings /usr/lib64/libssl.so |grep OpenSSL`
#### 3 配置
* 在/etc/ld.so.conf文件中写入openssl库文件的搜索路径（先检查是否已经配置好）
`echo "/usr/local/ssl/lib" >> /etc/ld.so.conf`
* 使修改后的/etc/ld.so.conf生效 
`ldconfig -v`
#### 4 查看现在openssl的版本是否是升级后的版本,并重启依赖openssl的服务
* `openssl version`
* 此外还需要重启其他与OpenSSL相关的服务
* 命令选项  
![](../assets/openssl-options.png)
* 参考 [官网](https://www.openssl.org/source/)
## 实战
1. 生成 rsa 私钥  （原始私钥）
`openssl genrsa -out rsa_privateKey.pem 1024`
* 文件内容如图：  
![](../assets/rsa-privateKey.png)
2. RSA私钥转换成PKCS8格式  
`openssl pkcs8 -topk8 -inform PEM -in rsa_privateKey.pem -outform PEM -nocrypt`
* std 输出   
![](../assets/rsa-to-pkcs8.png)

* 使用该命令，将私钥转成PKCS#8格式，但原rsa_privateKey.pem文件中的私钥字符串并没有任何变化。但控制台输出的private key，跟rsa_privateKey.pem文件中的private key，不一样。若需使用PKCS8格式的私钥，即控制台中显示的私钥，将其拷贝出来即可。
* 注意，begin 与end 区别
3.  在转换的时候对私钥加密  
`openssl pkcs8 -topk8 -inform PEM -in rsa_privateKey.pem -outform PEM`   
去掉 -nocrypt 选项即可  
* 此时，控制台打印出的内容  
-----BEGIN ENCRYPTED PRIVATE KEY-----开头，-----END ENCRYPTED PRIVATE KEY-----结尾的字符串，这个就是加了密的PKCS#8格式的私钥。  因为输入了密码，转换后的字符串不一样，会比加了-nocrypt的长一些，所以原来的程序解析不了该私钥字符串，会出错。 
* 注意，begin 与end 区别
4. 生成与rsa原始私钥对应的RSA公钥  
` openssl rsa -in rsa_privateKey.pem -pubout -out rsa_publicKey.pem`
* 如图   
![](../assets/rsa-publicKey.png)
### 从apiclient_cert.p12中导出证书部分的文件，为pem格式
* `openssl pkcs12 -clcerts -nokeys -in apiclient_cert.p12 -out apiclient_cert.pem`
* 文件内容如图
![](../assets/pkcs12-cert-pem.png)
### 从apiclient_key.pem中导出密钥部分的文件，为pem格式
* `openssl pkcs12 -nocerts -in apiclient_cert.p12 -out apiclient_key.pem`
* 文件内容如图
![](../assets/pkcs12-pkcs8-pem.png)
## Java使用pem文件内容，示例代码
```java
1）私钥签名
a）获取私钥
//获取KeyFactory，指定RSA算法
KeyFactory keyFactory = KeyFactory.getInstance("RSA");
//将BASE64编码的私钥字符串进行解码
BASE64Decoder decoder = new BASE64Decoder();
byte[] encodeByte = decoder.decodeBuffer(priKey);
//将BASE64解码后的字节数组，构造成PKCS8EncodedKeySpec对象，生成私钥对象
PrivateKey privatekey = keyFactory.generatePrivate(new PKCS8EncodedKeySpec(encodeByte));
        
b）使用私钥，对数据进行签名
         //获取Signature实例，指定签名算法（本例使用SHA1WithRSA）
Signature signature = Signature.getInstance("SHA1WithRSA");
//加载私钥
signature.initSign(privatekey);
//更新待签名的数据
signature.update(plain.getBytes("UTF-8"));
//进行签名
byte[] signed = signature.sign();
//将加密后的字节数组，转换成BASE64编码的字符串，作为最终的签名数据
BASE64Encoder encoder = new BASE64Encoder();
return encoder.encode(signed);
 
2）公钥验签
a）获取公钥
//获取KeyFactory，指定RSA算法
KeyFactory keyFactory = KeyFactory.getInstance("RSA");
   //将BASE64编码的公钥字符串进行解码
BASE64Decoder decoder = new BASE64Decoder();
byte[] encodeByte = decoder.decodeBuffer(pubKey);
//将BASE64解码后的字节数组，构造成X509EncodedKeySpec对象，生成公钥对象
PublicKey publicKey = keyFactory.generatePublic(new X509EncodedKeySpec(encodeByte));
 
b）使用公钥，进行验签
//获取Signature实例，指定签名算法(与之前一致)
Signature signature = Signature.getInstance("SHA1WithRSA");
//加载公钥
signature.initVerify(publicKey);
//更新原数据
signature.update(plain.getBytes("UTF-8"));
//公钥验签（true-验签通过；false-验签失败）
BASE64Decoder decoder = new BASE64Decoder();
returnsignature.verify(decoder.decodeBuffer(sign));
        
         备注：
验签时，签名数据需要先BASE64解码
```

## [java keytool证书工具使用小结](http://www.micmiu.com/lang/java/keytool-start-guide/)
## JKS_密钥对生成与读取方法[转载](http://blog.csdn.net/xiao_zhu_kuai_pao/article/details/45441853)
## https双向认证，客户端使用与服务端协商好的自签证书
参考微信支付文档,和ClientCustomSSL.java, `../assets/下相关文件`