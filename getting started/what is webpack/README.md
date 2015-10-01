<h1>什么是webpack</h1>
webpack是近期最火的一款模块加载器兼打包工具，它能把各种资源，例如JS（含JSX）、coffee、样式（含less/sass）、图片等都作为模块来使用和处理。 

<img src="what-is-webpack.png" alt="">

<h1>为什么又另外一个模块加载/打包器出现？</h1>
现有的模块加载器是不太适合大项目的(如单页面应用)。主要原因是其它的模块加载器无法很好的实现拆分代码还有跟现在的一些静态资源一同进行打包模块化。

<h2>目标</h2>
<ul>
	<li>把依赖树拆分成模块，只在需要的时候才加载</li>
	<li>初始加载快</li>
	<li>每一个静态的资源(如css, 图像，web文字)会是一个模块</li>
	<li>可以把第三方库当成模块使用</li>
	<li>可以自定义模块部分</li>
	<li>适合大项目</li>
</ul>

<h2>webpack哪里不同？</h2>

<h3><a href="https://webpack.github.io/docs/code-splitting.html">代码分割</a></h3>
webpack有两种类型依赖关系: 同步与异步。异步依赖作为分割点，形成一个新的块，在优化了块树，每一块都一个文件被释放。

了解更多<a href="https://webpack.github.io/docs/code-splitting.html">代码分割</a>

<h3><a href="https://webpack.github.io/docs/loaders.html">加载器</a></h3>
webpack 只能处理javascript原生代码，但是加载器可以把其它资源转换成javascript, 这样，每一个资源就可以形成一个模块。

了解更多 <a href="https://webpack.github.io/docs/using-loaders.html">加载器使用方法</a>和<a href="https://webpack.github.io/docs/loaders.html">加载器</a>

<h3>巧妙解析</h3>
webpack 有一个聪明的解析机制，它几乎可以处理每一个第三方库。它甚至允许表达式中的依赖关系，比如: <b>require("./templates/" + name + ".jade")</b>。它处理着最常见的模块风格: <a href="https://webpack.github.io/docs/commonjs.html">CommonJS</a>和<a href="https://webpack.github.io/docs/amd.html">AMD</a>.
了解更多 <a href="https://webpack.github.io/docs/context.html">表达式中的依赖关系</a>，<a href="https://webpack.github.io/docs/commonjs.html">CommonJS</a>和<a href="https://webpack.github.io/docs/amd.html">AMD</a>.

<h3>插件系统</h3>
webpack有很多功能丰富的插件系统，大多数内部功能都基于这个插件系统，它允许你根据你的需求和开源的通用插件进行分发。

了解更多 <a href="https://webpack.github.io/docs/plugins.html">插件</a>


完...