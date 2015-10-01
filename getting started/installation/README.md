<h1>安装</h1>

<h3>node.js</h3>
安装 <a href="https://nodejs.org/en/">node.js</a>

<h3>webpack</h3>
webpack 可以通过 npm 来安装:
```
$ npm install webpack -g
```
通过上面的命令， webpack已经安装在全局中，接下来就可以使用webpack命令了。

<h2>在项目中使用webpack</h2>
最好webpack也作为项目中的依赖，通过这个你可以选择一个本地的webpack版本而不用强制去使用全局的那一个。

使用npm 增加一个 package.json 的设置文件:
```
$ npm init
```

安装并添加webpack至package.json:
```
$ npm install webpack --save-dev
```

<h2>版本</h2>
有两种webpack版本，一个是稳定版，一个是测试版。
测试版本用 -beta 来进行版本标注。测试版本可能包含不太稳定的元素或一些正在实验开发的功能。查看<a href="https://webpack.github.io/docs/changelog.html">更新日志</a>。假如你想严格使用，请使用稳定的版本:

```
$ npm install webpack@1.2.x --save-dev
```

<h2>开发工具</h2>
假如你想使用开发工具，你可以通过命令行来安装:
```
$ npm install webpack-dev-server --save-dev
```

完...
