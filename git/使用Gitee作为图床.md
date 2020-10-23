# 使用Gitee作为图床

Markdown 用起来很方便，我一直很喜欢使用它来做笔记。但在引入图片的时候，markdown 为了让文件轻量化，选择了引用图片的方式。这一方式带来的后果是要在本地管理 markdown 文件所引用的图片，如果图片存放路径改变，相应的要修改引用该图片的 markdown 文件。另外如果想将 markdown 文件分享给别人，或者写到博客上，都会引用不到图片。

其中一种解决这个问题的方法就是使用图床。我选择使用 Gitee 创建一个存放图片的仓库，来作为图床。

## 操作步骤

1. Gitee 上创建一个名为 img-bed 的仓库
2. 开通 Gitee Pages 服务

![](https://gitee.com/Zed-cctw/img-bed/raw/master/img/img-5.png)

![](https://gitee.com/Zed-cctw/img-bed/raw/master/img/img-6.png)

3. 将图片存放在仓库中，点击图片文件，然后点击原始数据，这时复制地址栏中的url作为图片引用地址即可。

   ![](https://gitee.com/Zed-cctw/img-bed/raw/master/img/img-7.png)

4. Markdown 引用图片方法

   `![](url)`