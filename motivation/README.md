<a href="https://webpack.github.io/docs/motivation.html">原文链接</a>

<h1>动机:</h1>
前言：为什么需要webpack? webpack产生的动机是？

在这个时代，越来越多的网站已经开始进化成web应用了:
<ul>
  <li>越来越多的javascript运用在页面</li>
  <li>在现代的浏览器上实现更多的功能</li>
  <li>更少的整页重加载</li>
</ul>

结果必然是会导致客户端上存在着大量的代码需要去维护、开发。

大量的代码库需要被组织起来，所以模块系统提供了一个选择，它将可以把你的代码模块划分为各个小模块。

<h1>模块系统风格</h1>
有很多不同的标准去定义依赖关系和导出值:
<ul>
  <li>script 标签 风格(非模块系统) </li>
  <li>CommonJS</li>
  <li>AMD</li>
  <li>ES6 模块</li>
  <li>还有更多...</li>
</ul>

<h2>script 标签风格</h2>
如果你没有使用模块系统，你可以用这样的传统方式去处理一个模块化的代码库。
```
<script src="module1.js"></script>
<script src="module2.js"></script>
<script src="libraryA.js"></script>
<script src="module3.js"></script>
```

模块导出到全局对象的接口， 即window对象。模块可以访问全局对象的依赖借口。

<h3>常见问题</h3>
<ul>
  <li>得注意全局对象是否冲突</li>
  <li>得注意文件加载顺序</li>
  <li>开发人员必须解决模块/库之间的依赖关系</li>
  <li>在大型项目下，代码/文件将会越来越庞大并且后期将难以维护</li>
</ul>

<h2>CommonJS: 同步加载</h2>
这种风格使用了同步的方法来require加载依赖并返回一个输出接口。模块可以通过添加属性来指定export对象或者设置module.export的值
```
require("module");
require("../file.js");
exports.doStuff = function() {};
module.exports = someValue;
```
<a href="https://nodejs.org/en/">node.js</a> 就是使用这种服务器端的js.
<h3>优势:</h3>
<ul>
  <li>服务器端模块可以重用</li>
  <li>已经有很多这种风格的模块(npm)</li>
  <li>非常简单、易用</li>
</ul>
<h3>缺陷:</h3>
<ul>
  <li>阻塞调用不太适合于网络环境，因为网络请求是异步的</li>
  <li>不能并行加载多个模块</li>
</ul>

<h3>实践</h3>
<ul>
  <li><a href="https://nodejs.org/en/">node.js</a>  (服务器端)</li>
  <li><a href="https://github.com/substack/node-browserify">browserify</a></li>
  <li><a href="https://github.com/medikoo/modules-webmake">modules-webmake</a> (编译成一个包)</li>
  <li><a href="https://github.com/substack/wreq">wreq</a> (客户端)</li>
</ul>

<h2>AMD: 异步加载</h2>
异步加载解决了浏览器并行下载的问题，并且也有方法可以去定义模块还有导出值，如下面例子:
```
require(["module", "../file"], function(module, file) { /* ... */ });
define("mymodule", ["dep1", "dep2"], function(d1, d2) {
  return someExportedValue;
});
```
<h3>优势</h3>
<ul>
  <li>适用于网络中的异步请求方式</li>
  <li>多个模块并行加载</li>
</ul>

<h3>缺陷</h3>
<ul>
  <li>编码开销大（额外代码多）</li>
  <li>更难读写</li>
</ul>

<h3>实践</h3>
<ul>
  <li><a href="http://requirejs.org/">requirejs</a></li>
  <li><a href="https://github.com/cujojs/curl">curl</a></li>
</ul>

了解更多commonjs和amd 模式，在这里推荐阮一峰老师的好文：
<a href="http://www.ruanyifeng.com/blog/2012/10/asynchronous_module_definition.html">传送门</a>

<h2>ES6 模块:</h2>
为了支持支持模块系统，ecmaScript6 增加了一些新的语法来支持它
```
import "jquery";
export function doStuff() {}
module "localModule" {}
```
<h3>优势</h3>
<ul>
  <li>静态分析简单</li>
  <li>未来ES的标准</li>
</ul>

<h3>缺陷</h3>
<ul>
  <li>本地浏览器支持需要时间</li>
  <li>暂时还很少有运用es6风格的模块</li>
</ul>

<h2>数据传输</h2>
由于客户端需要执行模块，因此模块必须从服务器传输到浏览器。

传输模块有2种极端方式:
<ul>
  <li>每个模块为一个请求</li>
  <li>所有模块打包成一个请求</li>
</ul>

两种都是被广泛使用的，但是两者都不是最佳方式:
<ul>
  <li>
    每个模块为一个请求
    <ul>
      <li>优势: 只有需要的模块才会被传输</li>
      <li>缺陷: 太多请求开销导致页面请求阻塞延迟，应用启动慢</li>
    </ul>
  </li>
  <li>
    所有模块来自一个请求
    <ul>
      <li>优势: 少量请求开销，少量阻塞延迟，页面加载快</li>
      <li>缺陷: 不需要的模块也会被传输</li>
    </ul>
  </li>
</ul>

<h2>分块传输</h2>
看过上面两种方式后，肯定大家会觉得上面两种方式都不是很靠谱，假如有另外一个更灵活的传输方式会更好，即在大多数情况下，两种方式都可以互相妥协、互补。

比如：编译所有模块时，可以把模块分成多个更小的块

这样的话，我们可以得到多个较小的文件请求，不必要的模块只会在需要加载的页面下才会被请求，初始请求不会加载全部的代码库。

备注：这个想法是来自谷歌的<a href="https://developers.google.com/web-toolkit/doc/latest/DevGuideCodeSplitting">GWT</a>

了解更多 <a href="https://webpack.github.io/docs/code-splitting.html">代码分割</a>

<h1>为什么只有javascript?</h1>
为什么模块系统只帮助开发者去模块化js而已？实际项目开发上还有很多静态资源也需要一起被模块化，如:
<ul>
  <li>css样式</li>
  <li>图像</li>
  <li>web字体</li>
  <li>html模版</li>
  <li>更多...</li>
</ul>

还有:
<ul>
  <li>coffeescript 转换成 javascript</li>
  <li>less/sass 样式 转换成 css 样式</li>
  <li>jade templates → javascript which generates html</li>
  <li>i18n files → something</li>
  <li>更多...</li>
</ul>

这些应该也要有简单的方式去加载，如:
```
require("./style.css");
require("./style.less");
require("./template.jade");
require("./image.png");
```

了解更多 <a href="https://webpack.github.io/docs/using-loaders.html">加载器使用方法</a>和<a href="https://webpack.github.io/docs/loaders.html">加载器</a>


以上的种种原因就是产生webpack的动机。