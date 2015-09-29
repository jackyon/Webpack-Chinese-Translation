WEBPACK DEV SERVER:

webpack-dev-server 是一个轻量的node.js Express服务器, 它采用了webpack-dev-middleware来进行webpack打包。它的运行环境是通过socket.io来连接到服务器的。socket.io会向客户端发出编译状态的信息，然后这些信息会对这些事件作出反应。你可以根据项目的需求选择不同的模式。打个比方你有下面这些配置文件：

var path = require("path");
module.exports = {
  entry: {
    app: ["./app/main.js"]
  },
  output: {
    path: path.resolve(__dirname, "build"),
    publicPath: "/assets/",
    filename: "bundle.js"
  }
};

你有一个 app 文件夹，里头有你的所有初始化入口文件，这些文件将会统一捆版打包至根目录的 build 文件夹中。


<h2>Content Base:</h2>
webpack-dev-server 将会以当前目录运行这些文件，除非你特别声明了个特殊路径给content base， 如：
$ webpack-dev-server --content-base public/

当你用上面的语句特别声明了content base后，webpack-dev-server将会以 pubilc为默认目录来运行文件。它会自动监听所有你的源文件变化，当有发生改动时，它会自动重新编译打包。这个修改的打包文件是在指定的 publicpath 相对路径（查看api）， 它不会被写入到配置的输出目录 pubuilc 中。

例如通过上面的配置，你的打包文件将在这个路径下： localhost:8080/assets/bundle.js


为了加载你的打包文件，你需要在 public 目录下创建一个 index.html 文件：
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <script src="bundle.js"></script>
</body>
</html>

浏览器来运行你的app：localhost:8080/ ，假如你像上面一样设置了 publicPath， 比如: pubilicPath: "/assets/" 的话，你需要打开 localhost:8080/assets/



<h2>自动刷新:</h2>
webpack-dev-server 支持多种模式去自动刷新你的页面：
- iframe 模式 (当页面发生变化时，以iframe的形式嵌入在页面，然后自动刷新页面)
- inline 模式 (当页面发生变化时，webpack-dev-server 会把更新内容内嵌到打包文件中，然后自动刷新页面)

这两种模式都支持热加载组件(打包文件通知浏览器更新部分更改内容，而不用整个页面重新刷新)。热加载组建能在运行中的app中动态地更新、注入新增加或更改的代码



<h3>iframe 模式:</h3>
使用 iframe 模式，你不需要任何额外的设置。只要在浏览器中打开 http://<host>:<port>/webpack-dev-server/<path>。 
例如之前上面的配置： http://localhost:8080/webpack-dev-server/index.html

－ 不用多余的设置
－ 顶部信息栏比较友好
－ url改变时，浏览器的网址栏不会发生改变



<h3>inline 模式:</h3>
使用 inline 模式，你得加上 --inline


额，暂时木有时间继续翻译。。。等我有时间再继续吧。。。



