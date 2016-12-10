#Step by Step学习React之一：Ubuntu下安装React环境#

>##简介##
>React 起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架，都不满意，就决定自己写一套，用来架设 Instagram 的网站。做出来以后，发现这套东西很好用，就在2013年5月开源了。由于 React 的设计思想极其独特，属于革命性创新，性能出众，代码逻辑却非常简单，而且非常灵活，可以引用在各种项目上，在web项目前后端都很很好的使用，现在还能通过它开发Native APP。所以，越来越多的人开始关注和使用，认为它可能是将来 Web 开发的主流工具。

>##安装nodejs##
>在ubuntu终端执行下面的命令可以按照node.js v6<br/>
>
    curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
    sudo apt-get install -y nodejs
>
>安装nodejs包含npm,所以我们不需要另外安装npm,可以执行<code>node -v</code>和<code>npm -v</code>查看安装版本：<br/>
>![node-npm](http://i.imgur.com/3r8xH8i.jpg)
>
>##创建React APP
>建设一个新的单页面React APP是开始React APP开发最快的开始方式。它自动设置您的开发环境，以便您可以使用最新的 JavaScript 功能，提供了一个很好的开发体验，和优化您的应用程序。
>    
    npm install -g create-react-app
    create-react-app react-demo
    cd react-demo
    npm start


>执行结果如图所示，然后你可以通过`http://localhost:3000/`访问应用。
>
>![](http://i.imgur.com/fIAJhop.jpg)
>
>React APP不处理后端逻辑或数据库;它只是创建一个前端构建管道，所以你可以使用任何你想要的后端。
>##增加React到现有项目中
>React可以作为一个javascript组件添加到你的项目中，而且您不需要对你的项目做任何修改。如果您想在nodejs环境下使用React,您还需要安装React包，但是React支持ES6和JSX，所以需要安装babel编译器。
>####安装React包
>
>     npm install --save react react-dom
>####安装babel
>
>     npm install --save-dev babel-core
>####创建 .babelrc配置文件
>您已经安装了babel包，但是您还不是使用它。您需要在您项目根目录中创建一个.babelrc 配置和启用一些插件。
>若要开始，您还需要安装最新的Preset来转换ES2015及以上。

>     npm install babel-preset-latest --save-dev
>然后在.babelrc中配置preset信息
>
>     {
        "presets": ["latest"]
    }
>####使用CDN
>如果您不想使用npm来管理管理客户端软件包，React还提供CDN托管。
>在页面中引用：

>    
    <script src="https://unpkg.com/react@15/dist/react.js"></script>
    <script src="https://unpkg.com/react-dom@15/dist/react-dom.js"></script>
>或
>
    <script src="https://unpkg.com/react@15/dist/react.min.js"></script>
    <script src="https://unpkg.com/react-dom@15/dist/react-dom.min.js"></script>




