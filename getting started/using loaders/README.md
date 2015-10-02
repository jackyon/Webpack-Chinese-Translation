<h1>加载器是什么？</h1>
加载器能够让你app里头各种资源文件自动进行转换，然后用正确的格式加载到浏览器中。

例如你可以利用加载器告诉webpack去加载CoffeeScript 或 JSX.

加载器特点:
<ul>
	<li>加载器可被链接, 它们被应用各种资源的管道中，加载器最终会返回javascript</li>
	<li>加载器可同步也可异步</li>
	<li>加载器在node.js中几乎可以处理任何事情</li>
	<li>加载器支持查询参数， 这样可以将配置参数传递给加载程序</li>
	<li>加载器可以扩展程序插件/正则去配置</li>
	<li>加载器可以通过npm发布或安装</li>
	<li>普通的模块可以导出成加载器</li>
	<li>加载器可以访问配置</li>
	<li>插件可以给加载器带来更多的功能</li>
	<li>加载器可以释放出任意附加文件</li>
	<li><a href="https://webpack.github.io/docs/loaders.html">等等</a>...</li>
</ul>

了解更多<a href="https://webpack.github.io/docs/list-of-loaders.html">加载器</a>

<h1>解析 加载器</h1>
加载器解析类似于模块，加载器导出的函数是基于node.js， 与javascript兼容。在一般情况下，你可以通过npm去管理加载器，但是你也可以让加载器像文件一样保存在你的应用里。

<h2>引用加载器</h2>
加载器通常会命名为 xxx-loader (xxx为加载器名称)。例如: json-loader。

你可以用全名去引用加载器或者用简写的名字(例如:json)

<h2>安装加载器</h2>
假如加载器在npm上，你可以通过以下命令来安装加载器:
```
$ npm install xxx-loader --save
```
或
```
$ npm install xxx-loader --save-dev
```

<h1>使用方法</h1>
在应用中使用加载器有多种方法:
<ul>
	<li>明确的在 require 中声明</li>
	<li>通过配置文件配置</li>
	<li>通过CLI配置</li>
</ul>

<h2>在require中使用加载器</h2>
<blockquote>
	提示：如果可能的话避免使用此方式，如果你的脚本运行的环境是不可知的(Node.js和浏览器)。使用指定加载器去配置。
</blockquote>
通过require去声明加载器是可以的(如define, require.ensure, 等等). 只需要通过<b>!</b>来分离加载器，每个部分都分别对应于当前目录:
```
require("./loader!./dir/file.txt");
// => uses the file "loader.js" in the current directory to transform
//    "file.txt" in the folder "dir".

require("jade!./template.jade");
// => uses the "jade-loader" (that is installed from npm to "node_modules")
//    to transform the file "template.jade"

require("!style!css!less!bootstrap/less/bootstrap.less");
// => the file "bootstrap.less" in the folder "less" in the "bootstrap"
//    module (that is installed from github to "node_modules") is
//    transformed by the "less-loader". The result is transformed by the
//    "css-loader" and then by the "style-loader".
```

<h2>配置</h2>
你可以通过配置文件绑定正则给加载器:
```
{
    module: {
        loaders: [
            { test: /\.jade$/, loader: "jade" },
            // => "jade" loader is used for ".jade" files

            { test: /\.css$/, loader: "style!css" },
            // => "style" and "css" loader is used for ".css" files
            // Alternative syntax:
            { test: /\.css$/, loaders: ["style", "css"] },
        ]
    }
}
```

<h3>CLI</h3>
你可以通过CLI绑定扩展插件给加载器:
```
$ webpack --module-bind jade --module-bind 'css=style!css'
```
上面这条命令是指加载器"jade"加载".jade"文件，加载器"style"还有"css"给css文件。

<h2>查询参数</h2>
通过查询字符串可传递查询参数给加载器。查询字符串时通过"?"插入在加载器中。如: <b>url-loader?mimetype=image/png</b>

注意: 查询字符串的格式取决于加载器，具体得查看加载器文档，多数加载器接受普通的查询参数格式(如: ?key=value&key2=value2)还有json 对象(如: ?{"key":"value","key2":"value2"})

<h3>在require中:</h3>
```
require("url-loader?mimetype=image/png!./file.png");
```

<h3>配置文件中:</h3>
```
{ test: /\.png$/, loader: "url-loader?mimetype=image/png" }
```
或者:
```
{
    test: /\.png$/,
    loader: "url-loader",
    query: { mimetype: "image/png" }
}
```

<h3>CLI</h3>
```
webpack --module-bind "png=url-loader?mimetype=image/png"
```