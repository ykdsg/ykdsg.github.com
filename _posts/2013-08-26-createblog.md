---
layout: post
title:  如果建立一个免费网站
date:   2013-08-26 17:55:11
---

##通过github page 免费搭建个人网站

###从哪得到免费的主机服务
github page可以提供主机服务支持jekyll，这个网上资料很多，使用jekyll从无到有搭建一个网站很容易，难的是怎么熟悉jekyll的语法。这方面中文资料比较少，不过官网的英文也还算简单。本网站使用的模板是展新同学开发的[kunka](http://www.zhanxin.info/jekyll/2013-08-11-jekyll-theme-kunka.html)  
可以参考:[通过GitHub Pages建立个人站点](http://www.cnblogs.com/purediy/archive/2013/03/07/2948892.html)  
 [markdown语法](http://wowubuntu.com/)

###从哪得到免费的域名
网站建好之后，就会想搞个自己的域名，毕竟github的域名别人一看上去就知道是使用github page的，显的不怎么专业哈。当然如果你有钱，你可以在万网啊，Godaddy上买一个牛逼的域名。我们要经济适用，可以弄一个免费域名。[.tk域名](http://www.dot.tk/) 。注册很方便会注册QQ号的都会注册。

###得到免费的dns服务
现在有了域名，也有了主机服务，但是怎么串起来，就是把域名解析到服务器上，这个需要DNS解析服务。目前很多提供免费解析的，比如国内的 [DNSPOD](http://www.dnspod.cn)。同样注册一个账号，然后在刚才注册的tk域名配置一下，
![域名上得dns设置](/images/createblog/tk_dns.png)
这个每个dns解析商都不同，上面是dsnpod的。接着还要设置dnspod里面的域名解析到ip，ip可以通过ping下上面的主机服务得到。
![dnspod设置服务器ip](/images/createblog/dnspod_ip.png)
这里如果是适用github page建立的主机服务的话还需要在跟目录下放一个CNAME文件，里面写上你的域名。这样就全部弄好了，等dns生效之后就可以通过域名访问你的网站了。

  这个也算是建站之后开张第一篇，之后还有很多东西要慢慢摸索。
