<h1>使用插件</h1>

<h2>内置插件</h2>
插件可通过webpack配置中设置属性来使用:
```
// webpack should be in the node_modules directory, install if not.
var webpack = require("webpack");

module.exports = {
    plugins: [
        new webpack.ResolverPlugin([
            new webpack.ResolverPlugin.DirectoryDescriptionFilePlugin("bower.json", ["main"])
        ], ["normal", "loader"])
    ]
};
```

<h2>其它插件</h2>
不是内置的插件可以通过npm来安装:
```
npm install component-webpack-plugin
```
装完之后可通过下面的方式去调用插件:
```
var ComponentPlugin = require("component-webpack-plugin");
module.exports = {
    plugins: [
        new ComponentPlugin()
    ]
}
```

延伸：
<ul>
	<li><a href="https://webpack.github.io/docs/list-of-plugins.html">插件列表</a></li>
</ul>

完...