Hexo+Github部署自己的个人博客
===

**1、准备工作**

你必须要有的

GitHub账号
安装node.js、npm和Git环境

**2、创建仓库**

新建一个名为你的用户名.github.io的仓库，比如说，如果你的github用户名是test，那么你就新建test.github.io的仓库（必须是你的用户名，其它名称无效），将来你的网站访问地址就是 http://test.github.io

**3、配置SSH key**

提交代码肯定要拥有你的github权限才可以，但是直接使用用户名和密码太不安全了，所以我们使用ssh key来解决本地和服务器的连接问题。

```
$ ssh-keygen -t rsa -C "邮件地址"
```

然后连续3次回车，最终会生成一个文件在用户目录下，打开用户目录，找到.ssh\id_rsa.pub文件，记事本打开并复制里面的内容，打开你的github主页，进入个人设置 -> SSH and GPG keys -> New SSH key：

  ![SSH key](https://github.comm/inkeds/inkeds.github.io/raw/master/images/222.png)

3.1、测试是否连接

```
$ ssh -T git@github.com # 注意邮箱地址不用改
```

如果提示Are you sure you want to continue connecting (yes/no)?，输入yes

3.2、配置登录信息

```
$ git config --global user.name "liuxianan"// 你的github用户名，非昵称
$ git config --global user.email  "xxx@qq.com"// 填写你的github注册邮箱
```

4、Hexo安装
很多命令既可以用Windows的cmd来完成，也可以使用git bash来完成，但是部分命令会有一些问题，为避免不必要的问题，建议全部使用git bash来执行；
hexo不同版本差别比较大，网上很多文章的配置信息都是基于2.x的，所以注意不要被误导；
hexo有2种_config.yml文件，一个是根目录下的全局的_config.yml，一个是各个theme下的；

4.1、安装

```
$ npm install -g hexo
```

4.2、初始化
在电脑任意位置新建hexo文件夹（名字随意，别误删），例如 D:\Git\Hexo

```
$ hexo init
```

hexo会自动下载一些文件到这个目录

4.3、相关指令

```
$ hexo new "标题" # 创建新文章
$ hexo clean # 清除缓存
$ hexo g # 生成静态
$ hexo d # 上传
```

常见命令

```
hexo new "postName" #新建文章
hexo new page "pageName" #新建页面
hexo generate #生成静态页面至public目录
hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）
hexo deploy #部署到GitHub
hexo help  # 查看帮助
hexo version  #查看Hexo的版本
```

缩写：

```
hexo n == hexo new
hexo g == hexo generate
hexo s == hexo server
hexo d == hexo deploy
```

组合命令：

```
hexo s -g #生成并本地预览
hexo d -g #生成并上传
```

4.4、修改主题
默认主题很丑

个人选择了：[NexT](https://github.com/theme-next/hexo-theme-next)

首先下载这个主题：（默认就在 D:\Git\Hexo ）

```
$ git clone https://github.com/theme-next/hexo-theme-next.git
```

修改_config.yml中的theme: landscape改为theme: next，然后重新执行hexo g来重新生成。

如果出现一些莫名其妙的问题，可以先执行hexo clean来清理一下public的内容，然后再来重新生成和发布。

4.5、上传设置
如果你一切都配置好了，发布上传很容易，一句hexo d就搞定，当然关键还是你要把所有东西配置好。

首先，ssh key肯定要配置好。

其次，配置_config.yml中有关deploy的部分：

正确写法：

```
deploy:
  type: git
  repository: git@github.com:inkeds/inkeds.github.io.git
  branch: master
```
  
4.6、上传出错
hexo d报如下错误的话：

Deployer not found: github 或者 Deployer not found: git
需要安装插件

```
npm install hexo-deployer-git --save
```

5、结尾
GitHub由于某问题，国内访问比较慢，不建议生产站点搭建。
