---
title: hexo简单操作
date: 2018-04-16 19:20:11
tags:
---
一. 简单的搭建

安装Hexo
npm install -g hexo
进入工作目录，进行初始化
cd 工作目录
hexo init
安装依赖包
npm install
运行
hexo server 
查看结果
http://localhost:4000/
二. github发布

创建github账户，假设账户为 xxxx
创建仓库，仓库的名称必须要注意：xxxx.github.io，其中xxxx为账户名
设置SSH keys：需要在git bash下输入如下命令
#查找是否存在SSH keys
ls -al ~/.ssh
#如果是windows下，文件的地址应该在c:\用户\.ssh下
#生成Key命令
ssh-keygen -t rsa -C "注册gitbhub的邮箱"      
#输入命令
 ssh-agent -s
ssh-add ~/.ssh/id_rsa
#如果这里出现了错误：Could not open a connection to your authentication agent.请执行下面的命令
eval `ssh-agent -s`
ssh-add
注意：在github中设置SSH key，粘贴的内容为id_rsa.pub文件中的内容
最后使用如下命令完成测试工作

ssh -T [git@github.com](mailto:git@github.com)
进行部署：
修改_config.yml文件： 可以戳一下这里
deploy:
  type: git
  repository: 这里设置github资源库的ssh地址
  branch: master
注意：这里的设置冒号后面必须有空格
执行如下命令：

hexo generate
hexo deploy
博客地址
http://xxxx.github.io xxxx为账号名
三. Hexo的操作命令

简化操作方法：

hexo n == hexo new            增加新文章
hexo g == hexo generate    生成静态文件
hexo s == hexo server         启动服务
hexo d == hexo deploy        部署
安装主题：这里使用一种主题next

；将主题安装在themes/next目录下
$ git clone [https://github.com/iissnan/hexo-theme-next](https://github.com/iissnan/hexo-theme-next) themes/next   
$ git clone [https://github.com/MOxFIVE/hexo-theme-yelee.git](https://github.com/MOxFIVE/hexo-theme-yelee.git) themes/yelee  
配置主题：
修改 _config.yml 文件中 theme: next

Hexo命令：

hexo list <type>        列出网站资料
hexo version               显示Hexo版本号
hexo clean                  清除缓存文件db.json和生成的静态文件public
Hexo参数：

hexo --debug   调试模式，调试信息输出到debug.log中
hexo --save   安全模式， 不载入插件和脚本
hexo --silent   简洁模式，隐藏终端信息
hexo --config custom.yml   自定义使用的配置文件
hexo --draft 显示草稿箱中的文章
四. Hexo写作

执行命令创建一篇新文章
hexo new [layout] <title>
布局（Layout）有三种默认布局：post, page, draft，可以自定义布局，自定义布局和post存储位置相同
post source/_posts
page source
draft source/_drafts
文件名称
默认以主题为文章名称，可以在配置文件中设置new_post_name 参数，改变默认的文件名称。
:title 标题，类似的内容还有 :year :month : i_month(月份无前导0) :day :i_day

关于草稿的问题
可以生成一个草稿： hexo new draft "文章名"
草稿发布： hexo publish "文章名"
草稿默认不会显示在页面上，可以加上--draft参数来进行显示；也可以通过 render_drafts 参数设置为true来预览草稿

关于模板
新文章会根据scaffolds目录中的对应文件来建立文件
模板文件为*.md 文件最上方，---分隔区域以上的部分，用于指定文件的变量，使用{{变量}}
layout, title, date, updated, comments(开启文章评论的功能), tags, categories, permalink

分类和标签
有的文章支持分类和标签，可以在模板中设置。

作者：hutou
链接：https://www.jianshu.com/p/124b3bf367f4
來源：简书
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
