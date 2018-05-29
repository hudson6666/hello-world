# My Public Keys

GPG Public Key


<strong>pub</strong>  2048R/<a href="https://keyserver.ubuntu.com/pks/lookup?op=get&amp;search=0x25AC0345B92902AF">B92902AF</a> 2017-03-20            
	 Fingerprint=DFFA 853F A6B9 5DBF 185B  9F96 25AC 0345 B929 02AF 

<strong>uid</strong> <span class="uid">LI JIAHAO &lt;lijiahao99131@gmail.com&gt;</span>         
sig  sig3  <a href="https://keyserver.ubuntu.com/pks/lookup?op=get&amp;fingerprint=on&amp;search=0x25AC0345B92902AF">B92902AF</a> 2018-04-19 __________ __________ <a href="https://keyserver.ubuntu.com/pks/lookup?op=vindex&fingerprint=on&search=0x25AC0345B92902AF">[selfsig]</a>

<strong>sub</strong>  2048R/D4AE21F0 2017-03-20            
sig sbind  <a href="https://keyserver.ubuntu.com/pks/lookup?op=get&amp;fingerprint=on&amp;search=0x25AC0345B92902AF">B92902AF</a> 2018-04-19 __________ __________ <a href="https://keyserver.ubuntu.com/pks/lookup?op=vindex&amp;fingerprint=on&amp;search=0x25AC0345B92902AF">[]</a>


SSH Public Key

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC9NAzyvX6Kjv0Xuy6ErhnaicgI6/HxAAnZLLc06QIk1RE9rEfsAqFI3QP5EWgq8nrKE5i/MyVI3Yf/9DSuoi4yHgtdPjmaniXJm1iejzn2oTmGO4DWfJithxc2/uq4ABH/VL5DhdROPzJX6xm1zwBqRXWhN99ylbu2AQGeyTd31E8cB/B+VrOjgQpvLnLG1lEtEdiaRltDhO8QJmguDmV6B3WS+4/IwBrQF7E4gdk88ZbY0blD+0O47BFzmcLD3Tctk9LuZHOng1AoJE/WD+otOKnnzqtxOG8bxzPFXgBlKS/7zjhazqx97wEDKmwjx7BDirV0jx9eOlnNZWCH9wff lijiahao@cooler-archlinux
```

## 说明

这部分是写给不熟悉 GPG 和 SSH 的人，如果你很熟悉他们，请无视。

### 非对称加密

> 非对称加密算法需要两个密钥：公开密钥（publickey）和私有密钥（privatekey）。公开密钥与私有密钥是一对，如果用公开密钥对数据进行加密，只有用对应的私有密钥才能解密；如果用私有密钥对数据进行加密，那么只有用对应的公开密钥才能解密。因为加密和解密使用的是两个不同的密钥，所以这种算法叫作非对称加密算法。

其中公开密钥称为“公钥”，私有密钥称为“私钥”。顾名思义，在实际实践中，公钥是公开的（如我亲自通过消息发给你、像上面这样贴在我的网站上，或是上传到密钥服务器等），而私钥是只存在所有者的电脑里的。

GPG 和 SSH 的密钥默认都是采用非对称的 RSA 加密演算法，得益于此，我可以将公钥发布在这里，来实现下面这些美妙的事情。

### GPG

> 1991年，程序员 Phil Zimmermann 为了避开政府监视，开发了加密软件 PGP。这个软件非常好用，迅速流传开来，成了许多程序员的必备工具。但是，它是商业软件，不能自由使用。所以，自由软件基金会决定，开发一个 PGP 的替代品，取名为 GnuPG。这就是 GPG 的由来。

GPG 有很多用途，主要包括签名和加密两部分。

签名是指我发布了一条消息（或文件等），通过使用私钥签名，可以向别人证实此消息的确是我创作的。其他人可以通过我的公钥来验证此签名。

加密是我通过使用别人的公钥对消息进行加密，来确保只有持有私钥的那个人能够解密该消息。

在实际使用中，也可以同时进行加密和签名，使得某条消息只能被我所设置的接收人解密，并且向他证明该消息的确是我发送的。

1. 安装

    在 Linux 系统中，通常自带 GnuPG，如果没有的话，通过包管理器安装即可，名字一般叫 gnupg。

    在 Windows 系统中，安装 Git Bash 通常即自带 GnuPG，打开 Git Bash 就可以使用。

2. 导入

    从公钥服务器中导入
    
    ```
    gpg --keyserver keyserver.ubuntu.com --recv-keys 25AC0345B92902AF
    ```
    
    手动导入
    
    复制[这里](https://raw.githubusercontent.com/rikakomoe/hello-world/master/pgp_keys.asc)的内容保存到一个文本文件，例如 lijiahao.asc，运行下面的命令即可导入我的 GPG 公钥。

    ```
    gpg --import lijiahao.asc
    ```

3. 加密

    如果你要在一个公开信道（如发表在公开的评论区）向我发送文件或消息，或是通过不信任的信道（如使用某些公司的软件，明文的电子邮件等）向我发送机密内容，
	可以使用 GPG 加密，来确保只有我能够解密。

    要加密一个文件，使它只有我能够解密，

    ```
    gpg -e -r lijiahao99131@gmail.com -o 1.zip.gpg 1.zip
    ```
	
    其中 -e 代表加密，-r 代表使用的公钥，-o 代表输出到的文件，最后是要加密的文件。

    对于要加密的消息，

    ```
    gpg -e -a -r lijiahao99131@gmail.com -o 1.txt.asc 1.txt
    ```
	
    -a 表示使用 ASCII 的方式输出。用记事本打开 1.txt.asc，然后把里面的内容发送给我就可以了。
  
4. 验证签名

    如果你在一个不受信任的平台下载了不明来源的文件，或是收到声称为“我”发送的消息，可以通过验证签名来证实是否是由我发出的。

    如果是我签名的文件，通过以下命令来验证是否是我签名的
   
    ```
    gpg -v 1.txt.gpg
    ```

    如果是我签名的消息，把它粘贴到一个文本文件里，然后通过此命令判断是否是我签名的
   
    ```
    gpg -v 1.txt.asc
    ```

    如果是单独的签名文件，把它和源文件一起传入来验证
   
    ```
    gpg -v 1.zip.gpg 1.zip
    ```
	
5. 其他

	以上只是对 GPG 的一个简单介绍，目的在于回答如果有人要问“这个 key 是干什么用的，怎么用”。
	如果你想要学习 GPG 的使用，如自己怎么生成一个 key，怎么进行签名等，可以参考这些链接：
	
	- [GPG入门教程- 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2013/07/gpg.html)
	- [The GNU Privacy Handbook](https://gnupg.org/gph/en/manual.html)
  
### SSH

> SSH 密钥对可以让您方便的登录到 SSH 服务器，而无需输入密码。由于您无需发送您的密码到网络中，SSH 密钥对被认为是更加安全的方式。再加上使用密码短语 (passphrase) 的使用，安全性会更上一层楼。

如果你需要让我登录你的主机，可以考虑将我的 SSH 公钥添加到你的 authorized_keys 里，这样我就可以从我的电脑上登录（而不需要密码）啦 :wink:

更多关于 ssh key 的使用，可以参考这个链接：

- [How To Set Up SSH Keys](https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2)

对于 Windows 用户，Windows 10 1803 起已经自带 openssh。如果你使用的是旧版系统，可以使用 PuTTY，但是我更推荐使用 Git Bash 里的 ssh :wink:
