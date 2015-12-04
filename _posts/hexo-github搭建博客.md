title: 'hexo+github搭建博客'
date: 2015-07-01 08:04:45  
tags:  
- hexo  
- github  
- 博客
---
这篇文章要做的事情就是当你输入www.yourwebsite.com这种地址后它会跳转你你指定的页面上来。

我将按照我搭建博客的过程来讲解。在搭建的过程中参考了知乎，百度，以及很多由hexo+github搭建的博客，之所以自己还要做一次记录，是因为在按照上面搭建时还是遇到了很多问题，有些可能是自己马虎，还有一些可能是随着时间的改变一些配置本身发生了变化。文章的最后会给出参考文章的链接。<!--more-->
#一：购买域名

这是搭建过程中唯一需要付费的一步，但是也是最重要的一步，所以最开始就购买了域名，我的域名就是个人名字加上.com的后缀。域名是在goDaddy上购买的。goDaddy的网站主页貌似经常发生变化，而且中文版和英文版也会有一些区别。最起码我在上面购买域名时见到的页面和网上的教程都不一样，所以这里就不截图了。只说了基本的步骤和一些处理支付不成功时的方法。

![goDaddy的中文主页](http://7xjunb.com1.z0.glb.clouddn.com/无标题.png)


1. 在goDaddy的主页上输入你想注册的域名以及它的后缀名，它会检测你想要注册的域名是否已经注册，因为互联网上域名必须是唯一的，所以如果你要注册的域名已经被注册了，你就只能改后缀或者改名字了。
2. 选择了域名后如果你选择的域名没有被注册接着就是进行支付了，支付时goDaddy会给你推荐一大堆的服务，并且这些服务可能最开始都是选中的，你可以把这些服务都给去掉。
3. 之前在网上看到有优惠码可以使用，于是我也在网上找了一些优惠码，结果是支付时不能使用支付宝支付，所以如果你使用了优惠码结果无法使用支付宝支付，那么就不要使用优惠码，而且现在.com的域名一年也就70块RMB不到。
4. 还有可能就是goDaddy页面的设置。Global设置中将country（国家）选为”China”，Currency（货币）选为“United States Dollar”即可在支付的时候显示支付宝付款选项，要注意，一定要这样选择才可以的，不要选择“Chinese Yuan”，如果你国家没有选择China或者货币没有选择USD，都会导致最后付款的时候没有支付宝选项。
5. 最后支付时可能还需要goDaddy的账号，注册一个就行了。所有网站的注册方式基本上都是一样的。
#二：安装git

第二步需要进行的操作是安装git以及注册一个github的账号，关于git和gitbub的详细学习可以参考[git教程-廖雪峰](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/)。里面有关git的知识讲解的很详细，因为以前就使用过git并且电脑上本来就装有git的客户端，所以我没在这上面花费太多时间，不过还是将基本的步骤列举下来。下面的内容来源于[如何搭建一个独立博客](http://cnfeat.com/2014/05/10/2014-05-11-how-to-build-a-blog/)。若果你的电脑上本身就装有git客户端并且拥有一个github账号，那么这一步的操作可以全部省略掉。
安装git客户端的目的是接下来下面这些操作中都需要使用git这个工具：


1. 上传代码到github中



2. 安装npm



3. 安装hexo及其插件



##注册GitHub
访问：http://www.github.com/
注册你的username和邮箱，邮箱十分重要，GitHub上很多通知都是通过邮箱的。
##配置SSH keys
我们如何让本地git项目与远程的github建立联系呢？用SSH keys。
###检查SSH keys的设置
首先我们需要检查你电脑上现有的ssh key：


> $ cd ~/.ssh 检查本机的ssh密钥


如果提示：No such file or directory 说明你是第一次使用git。
###生成新的SSH Key：


> $ ssh-keygen -t rsa -C "邮件地址@youremail.com"
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/your_user_directory/.ssh/id_rsa):<回车就好>


注意1: 此处的邮箱地址，你可以输入自己的邮箱地址；注意2: 此处的「-C」的是大写的「C」
然后系统会要你输入密码：


> Enter passphrase (empty for no passphrase):<输入加密串>
Enter same passphrase again:<再次输入加密串>


在回车中会提示你输入一个密码，这个密码会在你提交项目时使用，如果为空的话提交项目时则不用输入。这个设置是防止别人往你的项目里提交内容。

注意：输入密码的时候没有*字样的，你直接输入就可以了。

最后看到这样的界面，就成功设置ssh key了：

![](http://cnfeat.qiniudn.com/11.png)

###添加SSH Key到GitHub
在本机设置SSH Key之后，需要添加到GitHub上，以完成SSH链接的设置。

1. 打开本地C:\Documents and Settings\Administrator.ssh\id_rsa.pub文件。此文件里面内容为刚才生成人密钥。如果看不到这个文件，你需要设置显示隐藏文件。准确的复制这个文件的内容，才能保证设置的成功。
2. 登陆github系统。点击右上角的 Account Settings—->SSH Public keys —-> add another public keys
3. 把你本地生成的密钥复制到里面（key文本框中）， 点击 add key 就ok了
![](http://cnfeat.qiniudn.com/s12.jpg)
###测试
可以输入下面的命令，看看设置是否成功，git@github.com的部分不要修改：


> $ ssh -T git@github.com


如果是下面的反馈：


> The authenticity of host 'github.com (207.97.227.239)' can't be established.
RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
Are you sure you want to continue connecting (yes/no)?


不要紧张，输入yes就好，然后会看到：


> Hi cnfeat! You've successfully authenticated, but GitHub does not provide shell access.


###设置用户信息
现在你已经可以通过SSH链接到GitHub了，还有一些个人信息需要完善的。

Git会根据用户的名字和邮箱来记录提交。GitHub也是用这些信息来做权限的处理，输入下面的代码进行个人信息的设置，把名称和邮箱替换成你自己的，名字必须是你的真名，而不是GitHub的昵称。



> $ git config --global user.name "cnfeat"//用户名
$ git config --global user.email  "cnfeat@gmail.com"//填写自己的邮箱

#三：使用GitHub Pages建立博客
现在就尝试使用github来建立博客，首先登陆github，新建一个仓库，这个仓库的名字是githubusername.github.io。其中githubusername是自己的github账号。
创建这个仓库的目的是为了接下来将使用hexo创建的博客托管在github中，这样就不需要自己再额外的购买虚拟空间了。

#四：安装nodejs和npm
安装nodejs的过程很简单，直接下载window中对应的msi版本，这个版本会直接将安装的路径添加到环境变量中。并且最新的这个版本已经集成了npm，所以也不用像以前那样还需要安装npm了(npm指nodejs package manage)。
安装完成后可以按下面的方式检测是否安装成功：
![](http://7xjunb.com1.z0.glb.clouddn.com/npm.png)

#五：使用Hexo
##安装Hexo
接下来就是安装Hexo这个工具了。
首先打开git，通过下面的命令就可以一键安装Hexo了。
> $ npm install -g hexo

在我的电脑上它将hexo貌似安装到C:\Users\allan\AppData\Roaming\npm下了，但是这个暂时不会影响使用，所以也没深究下去。
##部署Hexo
在电脑中某个地方建立一个名字叫「Hexo」的文件夹，然后在此文件夹中右键打开Git Bash。
> $ hexo init

Hexo随后会自动在目标文件夹建立网站所需要的所有文件，并默认帮助创建一篇如果使用hexo的博客。

现在我们已经搭建起本地的hexo博客了，执行以下命令，然后到浏览器输入localhost:4000看看。


> $ hexo g
> 
$ hexo s

输入localhost:4000就可以在本地看到使用hexo自动搭建起来的博客了。
接下来要做的事情是将这个博客托管到github中，并将第一步中购买的域名映射到github中的项目中。

#六：域名映射到github中的仓库中
##添加CNAME文件
找到在第三步中定义的仓库githubusername.github.io，在仓库的根目录下新建一个文件CNAME，这个文件不要加后缀，然后在文件里面加上第一步注册的域名。github会将托管在上面的项目中的CNAME文件中域名与仓库相绑定，这样在网址栏中输入域名时才能找到gitbub中的仓库。

查询githubusername.github.io的ip地址，使用ping即可：
> ping githubusername.github.io

记录下githubusername.github.io的ip地址。
##添加DNS Service记录
接下来需要进行域名解析DNS的设置，这里使用很多人都推荐的DNSpod。使用DNSpod进行域名解析的工作，可以直接使用QQ账号登陆，不需要注册。
选择DNSpod的域名解析功能，将第一步购买的域名添加进去，然后修改这个域名的一些记录。最终需要自己设置两个A记录。分别是@和www，ip地址填上一步获取的ip地址，还有两个类型是NS的地址是DNSpod自动生成的也需要保留，并将它添加到goDaddy中。最终DNSpod的设置如下图：
![](http://7xjunb.com1.z0.glb.clouddn.com/dns.png)
上图红色部分是自己添加的记录，这个记录是关键，一定要添加对。
##在goDaddy中修改DNS地址
再次登录goDaddy账号，找到购买的域名，进入配置页面，选择Nameservers。将其修改成上一步DNSpod中类型为NS的那两个地址。
![](http://7xjunb.com1.z0.glb.clouddn.com/goDaddy.png)
如果对在这上面进行修改的步骤不是很清楚，可以参考[这篇博客](http://cnfeat.com/2014/05/10/2014-05-11-how-to-build-a-blog/)，但是goDaddy的设置菜单位置好像本来就在变化，所以只需要参考它的流程，至于那些页面可能本身就发生了变化。
#七：使用Hexo将代码提交到github仓库
这一步将hexo生成的博客上传到github仓库中，由于第六步已经实现了域名到github仓库的映射，所以当你在这一步将hexo编辑的博客上传到github仓库后，通过域名访问的就是你的博客了，而不是像第五步那样通过hexo编辑的博客只能在本地访问。

将hexo编辑的博客上传到github的关键是编辑第五步生成的Hexo文件夹下的_config.yml文件。在这个文件的最后配置好deploy信息：

我将我的配置信息列举出来：
> deploy:
> 
> type: git
>
>repo: git@github.com:allanxia/allanxia.github.io.git 
>
>branch: master

**编辑这个配置信息时一定要注意冒号后面有个空格**，如果不加这个空格会报错，这好像是一种语法要求，在_config.yml中修改任何东西都需要按照这个要求来编写。
然后执行

> hexo clean
> 
>hexo generate
>
>hexo deploy

注意：
hexo clean和hexo c是等价的

hexo generate和hexo g是等价的，表示生成博客的静态文件

hexo deploy和hexo d是等价的，表示将静态文件上传到_config.yml指定的deploy路径中，这里就是上传到github中。


执行完上面的命令后就可以通过在网址栏中输入你注册的域名从而访问到使用hexo编写托管在github上的博客了。这里需要注意的是部署到github上的可能有时无法立即查看到效果，需要过几分钟才能看到效果。最开始我以为自己什么地方配置错误了，但是通过localhost:4000地址访问博客是更改了的，结果过了一会儿通过域名访问博客也更改了。

主要参考的一些文章：

[如何搭建一个独立博客——简明Github Pages与Hexo教程](http://cnfeat.com/2014/05/10/2014-05-11-how-to-build-a-blog/)

[使用GitHub和Hexo搭建免费静态Blog](http://wsgzao.github.io/post/hexo-guide/)

[怎样将域名绑定到github pages 博客上](http://jingyan.baidu.com/article/3c343ff70fb6e60d3779632f.html)








