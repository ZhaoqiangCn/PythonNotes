# 群晖—-外部访问DDNS教程（第一部分）



> ## DDNS简单说就是自动更新域名解析中的A记录解析的IP地址，如果你并不频繁重启光猫的话，你的公网IP其实并不会频繁变化

## 1.关于公网IP

最开始验证自己是否有公网IP的时候真的是绕了一个大圈子，其实通过[http://www.ipip.net/](http://www.ipip.net/) 查询下来，只要你的IP开头不是”172，192，10″的应该就是公网IP，至于在万网查询到有两个IP地址根本不用去管它，楼主就是有两个并且非”10″的那个就是公网IP。

## 2.关于端口映射

作为小白一枚，一开始并不很理解端口映射，所以当不断ping自己的公网IP却一直不通的时候，一度就认为ISP给的是大内网，先后误解了联通了电信，因为ping不通可能是路由器默认设置就是禁ping的，或者相应端口就没有打开。网上可以找到很多端口扫描的网站，做完端口映射以后即可测试一下。

### 如何做端口映射

首先要清楚自己家里的网络拓扑结构。楼主家里是光猫拨号，下面接的路由器，路由器下面才是家里的网络设备，所以我们的NAS相当于处在二级路由下面，这样的话就要做两次端口映射。第一次是把群晖的端口映射到路由器的端口上，第二次是把路由器的端口映射到光猫上。

可以通过：[http://canyouseeme.org/](http://canyouseeme.org/) 检查端口是否已打开

#### DMZ

DMZ一次可以映射所有端口，并把主机暴露在网关中。反正楼主的路由器就这么设置了，然后在映射NAS的指定端口到路由器上。

#### 群晖常用端口

DSM的端口，Web端口，Cloud端口，VPN服务器端口，邮件服务器等等这些常用的端口映射出去即可。

此处是[_群晖官方的PortFowording视频_](https://nashome.cn:31000/sharing/IsGyFvk4V)。

## 3.域名

楼主是在阿里云注册的域名，所以后续OSS和CDN也都是用的阿里的。同时加9.9元还有两年的云解析VIP，有了自己的域名一切都好办了。首先去备案，阿里有一套完整的方案，顺着走几个工作日就可以搞定。之后如果不想用到DDNS代理商那么冗长的二级域名的话，还是申请一个自己的域名比较舒心。

## 域名解析

#### A记录:

又称IP指向，用户可以在此设置子域名并指向到自己的目标主机地址上，从而实现通过域名找到服务器。  
说明：·指向的目标主机地址类型只能使用IP地址。

#### CNAME:

通常称别名指向。可以为一个主机设置别名。比如设置test.domain.com，用来指向一个主机www.domainA.com那么以后就可以用test.domain.com来代替访问www.domainA.com了。  
说明：CNAME的目标主机地址只能使用主机名，不能使用IP地址;

##  4.DDNS

详细的DDNS配置请参考：[_群晖—-外部访问DDNS教程（第二部分）_](https://www.nashome.cn/270)

配置完DDNS后我们就可以使用DDNS域名+端口号的形式访问群晖上的服务了，如果不想每次在外面打开DSM的时候还要输入端口号：“http://example.synology.me:5000” 后续博主会分享具体方法。

