# 如何使用njumsc.github.io

## 前言

> 详细的博客搭建教程可以看[qiubaiying写的教程](https://www.jianshu.com/p/e68fba58f75c)

## 如何发布文章

### 快速开始

以下有两种方法：

#### 第一种：直接在网页上编辑博客

打开仓库地址https://github.com/njumsc/njumsc.github.io/tree/master/_posts 进入到_posts文件夹，点击create new file,创建你的.md文档。

#### 第二种：把仓库clone到本地后，新建一篇文章

将本项目fork到你的仓库，然后在Github Desktop打开在**你的仓库**中的这个项目

![QQ截图20190819181357.png](https://i.loli.net/2019/08/19/f6H7cnsDtvRE49Y.png)


![QQ截图20190819182157.png](https://i.loli.net/2019/08/19/36ODMfFIePwU5bH.png)

然后进入到这个项目的文件夹下，进入_post文件夹（这个文件夹就是我们放发表的文章的地方），新建一个.md文件，文件名为日期-文章名字.md（例如2019-08-19-2019年微软学生夏令营.md），用你喜欢的markdown编辑器打开它，例如Typora。

#### 为你的文章编写YAML头信息

![img1](https://i.loli.net/2019/08/19/mrRCLY7h6aNPF4T.png)

如果你用的是Typora，你可以在[段落]下找到[YAML front matter]，然后直接输入你的头信息，当然你也可以使用markdown代码的形式，例如这样：

![i2](https://i.loli.net/2019/08/19/b5zF9n8R4UO2Cd6.png)

这里解释一下YAML里各个参数的意义：

- layout代表你使用的模板，发表文章使用的都是post模板
- title代表文章的标题，这个发布后会显示在网站上
- subtitle代表子标题
- date是文章的发布日期，格式为year-month-date
- author是作者，使用的名字最好先进行注册（如何注册看[这里](#注册自己的作者标签)）
- jump-url是外链，一般可以没有，具体看[这里](#如何转载其他网站上的文章)
- tags是文章的标签，你可以给文章添加一些标签让你的文章更容易被找到



#### 编辑你的文章

将头信息填完后，就可以开始你的文章创作啦！

#### 图片问题：
由于md格式的限制，目前在文章中要插入图片有两种途径：
1. 用图床（一个帮你存图并分给你这个图的公网url的地方），那就插入图片url.(推荐的图床: 免费的sm.ms,阿里的半年五块钱)
2. 先上传图片到img文件夹，再从github中获取到这些图片的url,再插入你的.md文件
**img文件夹请尽量存缩略图，并且以Author-时间进行命名，存大量图片会导致clone速度极慢，msc的博客大家一起维护~**

#### 发布你的文章

##### 如果是在网页直接编辑
编辑完成后，在页面的最下方找到Propose file change的绿色button,点击后页面跳转，继续点击create new pull request,可以留下comment也可以不留，再次点击create new pull request确认即可

##### 如果是本地编辑

![QQ截图20190819190356.png](https://i.loli.net/2019/08/19/SweP9O2X3chIC1a.png)

文章写好以后打开Github Desktop，点击左下角的commit，更改就保存到了本地，然后点击上方的push（commit之后会变为push），就可以把你的文章发布在你的仓库里了。然后点击Branch -> create pull request,点击create new pull request绿色按钮,可以留下comment也可以不留，再次点击create new pull request确认即可。
然后等待仓库管理员确认你的pull request之后，访问[njumsc](http://njumsc.github.io)，就可以看到你刚发布的文章啦！
（如果看不见，可按ctrl+r 强制刷新)

#### *也可参考[这里](https://njumsc.github.io/2017/02/06/快速搭建个人博客/#写文章)，查看如何在web页面编辑后，发表文章*

### Tips：如何转载其他网站上的文章

如果想要把微信公众号或者其他一些外部网站的文章转到官博上要怎么做呢？

**方法一**：直接复制网页内容编辑成markdown的文件（在获得授权的情况下）

**方法二**：参考“2019年微软学生夏令营”的md文件，在YAML里使用jump-url标记文章的链接，然后在内容部分放上文章的摘要即可

---

## 注册自己的作者标签

注册作者标签之后在Author页面可以根据你的标签显示你发布过的文章，更利于内容的整合。

注册方式为，在项目目录下找到_config.yml文件，找到

```yml
authors:  # your site author
	- name: XXX   # your name 
	  github: XXXX # your github id
	  brief-intro: XXXX #个人简介 
```

按照同样的格式在后面加入你的信息即可（个人简介可暂时不填）

例如我是张三，github ID是ZHANG SAN

那么就是：

```yaml
authors:  # your site author
    - name: XXX   # your name 
      github: XXXX # your github id
      brief-intro: XXXX #个人简介 
    - name: 张三   # your name 
      github: ZHANG SAN # your github id
      brief-intro: 我，张三，一个么得感情的男人 #个人简介 
```



---

## License

遵循 MIT 许可证。有关详细,请参阅 [LICENSE](https://github.com/qiubaiying/qiubaiying.github.io/blob/master/LICENSE)。

