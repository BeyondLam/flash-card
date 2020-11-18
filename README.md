# 记忆手卡

![记忆手卡](https://cdn.hicaiji.com/lmp/flash_cards.jpg)

### 音宫有话说

>   这个项目是我自己最喜欢的一个项目之一
>
>   做这个项目的初衷是希望有一个平台能让大家在上面寻找和分享面经，并且是卡片形式来记载的面经知识点
>
>   用了一段时间发现，有些问题自己现阶段无法解决，比如说一些功能想添加或者修改，因为自己不太熟练小程序端开发，所以更新进度很慢，同时我又不希望这个项目烂在我手里，毕竟是一行一行代码敲出来的，它陪伴了我整个2020年的暑假
>
>   希望大家好好地对待**她** 

### 求赞

如果觉得这个项目有帮到你，**求给项目一个star**，让更多人知道这个项目



### 目标

既然开源了，就希望大家都能从这个项目中学到一些东西

大家可以随便改代码、加功能，代码随意使用，改成你们想改的都OK

我也是一路学习过来并且还在学习中的一枚**菜鸡**

如果有什么地方有bug或者设计有缺陷等等，都欢迎跟我讨论

这个项目我相信可以帮助一些刚使用flask不久或者想找个flask项目练练手的朋友

你们将能从这个项目中学到

-   flask中大型项目的一个结构（更加规范地开发）
-   token的使用
-   装饰器的使用
-   Sqlalchemy的增删查改
-   使用redis来模拟锁
-   写一份接口文档



### 软件架构

![](https://cdn.hicaiji.com/flash_card/flash_card_structure.png)

**核心功能点：**

-   新建、删除、查看、修改手卡（知识点卡片）
-   新建、删除、查看、修改卡集
-   可以标记卡片的状态（掌握、未掌握）
-   附件管理（图片管理）
-   克隆其他人分享的卡集
-   支持markdown渲染
-   其它...



**项目使用技术：**

-   Flask
-   Flask-SQLalchemy
-   Redis
-   Mysql
-   小程序
-   markdown渲染



### 安装教程

**1. 下载**

下载源代码
```shell
git clone https://github.com/BeyondLam/flash-card
```
进入到服务端代码目录
```shell
cd flash_card/server
```

**2. 配置虚拟环境**

```bash
python3 -m venv venv
```

**3. 激活虚拟环境**

```bash
source venv/bin/activate
```
**4. 安装依赖包**

```bash
pip install -r requirement.txt
```

**5. 创建数据库和导入数据库**

先在数据库创建一个数据库名 flash_card

进入到sql文件夹内
然后输入命令导入数据

```shell
mysql -uroot -p flash_card < flash_card.sql 
```

**6. 运行**

```bash
# 第一种部署 （测试和开发的时候用这种） (5000是端口)
python manage.py runserver -h 0.0.0.0 -p 5000

# 第二种部署 （线上环境推荐用下面这种 5050是端口，可以根据自己需要更改）
gunicorn -w 4 -b 0.0.0.0:5050 manage:app 
```

如果你看到下面这样子，那么你就部署成功了
![部署成功截图](https://cdn.hicaiji.com/halo/%E6%88%AA%E5%B1%8F2020-11-18%2015.19.54_1605684018981.png?image/auto-orient,1/resize,m_lfit,w_200/quality,q_90)


上面的只是跑起来的命令而已，代码里面的数据库、redis、小程序账号等等的配置要自己进config.py文件修改

下面**使用说明**会介绍一下怎么配置其他信息





**1 小程序配置**

小程序可以直接打开微信开发者工具就能运行

-   要修改的就是修改为自己的appid

-   修改接口的地址



### 使用说明

> 如果你根据上面的命令运行起来了，那么你就成功一半了
>
> 接下来就是配置你自己的信息



接下来一定要准备的东西有

-   mysql
-   redis
-   小程序appid和密码
-   腾讯云短信配置
-   腾讯云COS配置
-   微信小程序回调函数的token



**必须的三样东西**

Mysql、redis、小程序的appid和密码



**mysql （必须要）**

mysql 在config文件配置，主要是操作数据库要用的配置



 **redis （必须要）**

用来存一些缓存、手机短信验证码、用户访问限制频率



**小程序appid和密码 （必须）**

用来请求获得用户的openid



上面这三样能让你的后台接口大部分可以用



如果你需要图片上传、发送短信绑定手机号的功能

那么你要配置

-   腾讯云短信配置
-   腾讯云COS配置
-   微信小程序回调函数的token



**腾讯云的短信发送**

如果要绑定用户的手机号 即发短信 你要有发腾讯云短信的配置信息 可以在 【我的-点击头像-绑定手机】体验



**腾讯云COS信息配置**

这里主要是上传图片的cos配置，我的配置可能跟大家的一些域名配置什么的可能不一样

这些要去 ./app/utils/TXcos 文件夹下面看看代码实现，适当修改一些为你们自己的

比如看看有没有自己的域名的cdn域名等等，可以在腾讯云获取对应的上传图片的配置信息


**微信小程序回调函数的token**

如果要上传图片，还要去配置小程序的回调信息

可以去小程序管理平台-开发-开发设置-消息推送-启用-配置你的token

![获取token](https://cdn.hicaiji.com/lmp/img/token.png)

然后在config.py文件里面的

```
wx_mnp_token = 'xxx'  # 微信小程序回调函数的token
```

配置你的token





### 注意

>下面是我开发前写的接口文档
>拿出来的目的是，给大家可以稍微参考一下
>实际的接口可能跟接口文档有些出入，因为都是我自己一个人开发的
>
>所以接口文档可能有变化而我没去更改它
>
>如果你想给接口文档修改修改，欢迎提交给我哦～

### [接口文档](ApiDocuments.md)

[接口文档](ApiDocuments.md)





