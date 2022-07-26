> 本文由 [简悦 SimpRead](http://ksria.com/simpread/) 转码， 原文地址 [blog.csdn.net](https://blog.csdn.net/weixin_43408077/article/details/119617516)

### 1.[react](https://so.csdn.net/so/search?q=react&spm=1001.2101.3001.7020) 项目打包

#### 1.1 终端运行打包命令

在编辑器的终端运行 vue 项目打包命令

```
yarn build

```

打包成功如下：  
![](https://img-blog.csdnimg.cn/e082a61f3a9346b6871b15bb91d4cd79.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQwODA3Nw==,size_16,color_FFFFFF,t_70#pic_center)

这时我们可以看到项目目录多出来一个 build 文件夹，记住它，后面部署就靠它了。

#### 1.2 修改配置

在 package.json 里面添加一行：

```
"homepage": "."

```

如果不加上这个的话之后打包的时候, 打开 index.html 会报错，示例如下：

![](https://img-blog.csdnimg.cn/22a4515b1a6d47638253d1a56ae640a4.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQwODA3Nw==,size_16,color_FFFFFF,t_70#pic_center)

### 2. 宝塔面板部署项目

#### 2.1 部署要求

*   有一台云服务器（笔者这里用的是腾讯云）
*   服务器安装宝塔面板 **[安装教程](https://zhuanlan.zhihu.com/p/265941701)**

#### 2.2 在腾讯云开发端口

登录腾讯云，选择控制台，打开[云服务](https://so.csdn.net/so/search?q=%E4%BA%91%E6%9C%8D%E5%8A%A1&spm=1001.2101.3001.7020)器面板，选择安全组栏

![](https://img-blog.csdnimg.cn/b45386340fda4f5ba2a3a724bc426f1d.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQwODA3Nw==,size_16,color_FFFFFF,t_70#pic_center)

根据自己的安全组，通过**添加规则**开放一个端口给自己的项目, 示例如下：

![](https://img-blog.csdnimg.cn/img_convert/4ad004a1541b4d55ae9d1ffe54e70d77.png)

**注意**，入站规则和出站规则都要开放这个相同的端口。

#### 2.3 在宝塔上搭建个人网站

①、登录宝塔，在【网站】下选择【添加站点】；  
注：在域名里填写两行，第一行随便起一个域名，第二行填写 IP: 端口号。(**IP 为你的服务器的公网地址，端口号必须与你刚刚开放的端口号一致**)

![](https://img-blog.csdnimg.cn/e429f4b91f004a5cb2728ca33581ea50.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQwODA3Nw==,size_16,color_FFFFFF,t_70#pic_center)

②、点击刚刚新建的域名，可以看见【域名管理】下有两行，删除域名，只留 IP；

③、点击【文件】，在域名目录下（例如刚刚的 www.3434.com）上传第一步打包的 build 文件夹。

![](https://img-blog.csdnimg.cn/8734cc510abf48b4924506c030c09c0a.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQwODA3Nw==,size_16,color_FFFFFF,t_70#pic_center)

④、点击【网站】，点击刚刚新建的域名，选择【默认文档】，添加 build，一般网页默认 index.html 为首页，这里在【默认文档】里修改主页为 build，如下：

![](https://img-blog.csdnimg.cn/96573ebf2e0b474cb67cc16b6a587d99.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzQwODA3Nw==,size_16,color_FFFFFF,t_70#pic_center)

至此，宝塔面板部署项目成功！

### 3. 在浏览器打开项目

现在只需要在浏览器地址栏输入 **IP: 端口号**，(IP 为你的服务器的公网地址，端口号必须与你开放的端口号一致)，即可看到自己的项目，项目部署成功！

#### 4. 参考资料

[329 - 将 react 项目打包部署在服务器上](https://blog.csdn.net/qq_33781658/article/details/88966003)

[在宝塔上利用一个 IP 搭建多个个人网站](https://blog.csdn.net/weixin_45616775/article/details/111411054)

[宝塔–同一 IP 下架设多个网站](https://blog.csdn.net/weixin_44567104/article/details/102485265?utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.control)