# Node.js

* **什么是Node**

  ​	在 V8 引擎基础上套了一层壳，通过编写 JS 代码可以实现后端能做的事情

  ​	特点：事件驱动、非阻塞的I/O等特性

  ​	优势：轻量、高效

  ​	官网：[https://nodejs.org/en/](https://nodejs.org/en/)

* **Node的安装**— 3m安装法

  1. [nvm](https://github.com/creationix/nvm) （Node Version Manager）

  ​	   	 解决多版本共存、切换问题

  2. [npm](https://github.com/npm/npm)   (Node Package Manager)  

  ​		 解决 Node.js 模块安装问题

  3. [nrm](https://github.com/Pana/nrm)    (NPM Registry Manager)

  ​		解决 npm 镜像访问慢，提供测试，切换

  **NVM**

  ​	curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash

  ​	下载nvm, 并将路径配置到 ~/.bashrc 中

  ​	注: 如果终端是zsh，则需要配置到~/.zshrc 中(可通过 echo $0 查询)

  ​

  **NVM 常用命令**

  ​	nvm  --version  查看当前版本

  ​	nvm ls 查看当前已安装 node 的版本

  ​	nvm ls-remote 查看远程 node 的版本

  ​	nvm install 4.4.5 安装某版本 node	

  ​	nvm use 4.4.5 使用某版本 node 

  ​	nvm alias default 4.4.5 把某版本 node 设为默认值

  ​

  **NPM**

  ​	**NPM使用介绍**

  ​		NPM是随同NodeJS一起安装的包管理工具，能解决NodeJS代码部署上的很多问题，常见的使用场景有以下几种：

  - 允许用户从NPM服务器下载别人编写的第三方包到本地使用。
  - 允许用户从NPM服务器下载并安装别人编写的命令行程序到本地使用。
  - 允许用户将自己编写的包或命令行程序上传到NPM服务器供别人使用。

  由于新版的nodejs已经集成了npm，所以之前npm也一并安装好了。同样可以通过输入 **"npm -v" **来测试是否成功安装。命令如下，出现版本提示表示安装成功:

  ​	安装完 Node 后自带 npm

  ​	npm -v 查询当前npm版本

  ​	npm install npm -g 通过 npm 更新 npm

  ​	npm install 模块名 

  ​	[常用 npm 模块一览](https://github.com/ruanyf/articles/blob/master/2015/2015-04-04-npm-modules.md)

  **NRM**

  ​	npm install -g nrm

  ​	nrm test 

  ​	nrm ls

  ​	nrm use taobao

  ​


* **第一个Node程序**

  如果我们使用PHP来编写后端的代码时，需要Apache 或者 Nginx 的HTTP 服务器，并配上 mod_php5 模块和php-cgi。

  从这个角度看，整个"接收 HTTP 请求并提供 Web 页面"的需求根本不需 要 PHP 来处理。

  不过对 Node.js 来说，概念完全不一样了。使用 Node.js 时，我们不仅仅 在实现一个应用，同时还实现了整个 HTTP 服务器。事实上，我们的 Web 应用以及对应的 Web 服务器基本上是一样的。

  在我们创建 Node.js 第一个 "Hello, World!" 应用前，让我们先了解下 Node.js 应用是由哪几部分组成的：

  1. **引入 required 模块：**我们可以使用 ``require`` 指令来载入 Node.js 模块。

  2. **创建服务器：**服务器可以监听客户端的请求，类似于 Apache 、Nginx 等 HTTP 服务器。

  3. **接收请求与响应请求** 服务器很容易创建，客户端可以使用浏览器或终端发送 HTTP 请求，服务器接收请求后返回响应数据。

     **创建 Node.js 应用**

     步骤一、引入 required 模块

     我们使用 **require** 指令来载入 http 模块，并将实例化的 HTTP 赋值给变量 http

     步骤二、创建服务器

     接下来我们使用 http.createServer() 方法创建服务器，并使用 listen 方法绑定 8888 端口。 函数通过 request, response 参数来接收和响应数据。

  ```javascript
  //引入系统模块 http
  var http = require("http");
  //创建服务
  http.createServer(function (req,res) {
      //响应内容
      res.end("Hello,Node.js");
      //监听端口3000
  }).listen(3000);
  ```

  ​

* **Common JS规范**

  1.console.js

  ```javascript
  var console1 = require('console');
  console1.log('hahaha');
  //info与log等价
  console.info('hah');

  //1.输出日志
  console.log('班长看小黄图');
  //2.输出断言，有开发者定义错误内容
  // console.assert(1 === 100,'1绝对不等于100');//输出错误
  // console.assert(1 !== 100,'1绝对不等于100');//不输出错误

  var obj = {
      name:'张三',
      age:100,
      sex:'2'
  }

  var obj2 = new Object();
  obj2.name = '李四';
  obj2.setName = function (name) {
      this.name = name;
  }
  //3.用来打印对象
  console.dir(obj2);
  //4.用来打印错误
  console.error('你报错了！！！');
  console.error(new Error('出错啦'));
  console.log(new Error('出错啦'));
  //warn和error等价
  console.warn('你报错啦！！！');

  //5.time 和 timeEnd (成对存在)
  console.time('timer');
  for(var i= 0;i<100000;i++){

  }
  console.timeEnd('timer');

  //6.trace
  console.trace('当前栈信息');

  ```

  2.global.js

  ```javascript
  //Node.js中的全局变量

  //1.当前 模块（js文件） 所处目录
  console.log(__dirname);// /Users/dllo/Desktop/Node/1Node01
  //__filename 表示当前正在执行的脚本的文件名。它将输出文件所在位置的绝对路径，且和命令行参数所指定的文件名不一定相同。 如果在模块中，返回的值是模块文件的路径。

  //2.当前 模块（js文件） 的绝对路径
  console.log(__filename);// /Users/dllo/Desktop/Node/Node01/global.js

  //3.定时器相关 （详见timer）

  //4.console详见 console.js

  //5.exports 属于module.export 的简短引用（详见模块引用）

  //6.global 全局对象 类似于浏览器中的window,但不同

  // var a = 10;//global.a 是访问不到的
  a = 10;//向上层寻找a 找不到就是在global定义
  console.log(a);
  console.log(global.a);

  //global中包含很多内容，不要轻易往其中存储内容
  console.log(global);

  //7.module 代表当前模块（js）本身
  console.log(module);

  //8.process 进程对象

  //9.require 引入模块，具体和exports、module一起讲解

  ```

  3.NodeJS和CommonJS之间的关系

  ​	CommonJS是一种规范，而Node.js是这种规范的实现

  ​	Node.js只是实现了部分CommonJS的规范



