# 那些常见的 loader

#### 什么是loader?
loader是模块转换器，可以理解为翻译。

#### 为什么Webpack需要loader?

Webpack的最终目之一是把代码翻译成浏览器能读懂的语法，loader就是做这个事情的。

#### loader的执行顺序

loader执行包括两个阶段，pitch阶段和normal阶段。Normal阶段，就是大家一般认为的loader对源文件进行转译的阶段。Pitch阶段会先于normal阶段进行，如果loader定义了pitch方法，就会在pitch阶段被执行；如果loader的pitch方法返回了内容，则会跳过后方loader的pitch和normal阶段。

#### 控制loader的执行顺序
pitch方法为loader提供了跳过某些执行阶段的能力。

#### postcss-loader
它提供了一种方式用 JavaScript 代码来处理 CSS。它负责把 CSS 代码解析成AST，再交由插件来进行处理。插件基于CSS 代码的 AST 所能进行的操作是多种多样的，比如可以支持变量和混入（mixin），增加浏览器相关的声明前缀，或是把使用将来的 CSS 规范的样式规则转译（transpile）成当前的 CSS 规范支持的格式。从这个角度来说，PostCSS 的强大之处在于其不断发展的插件体系。
1. 给css属性名添加浏览器前缀
2. 压缩css

#### babel-loader
此 package 允许你使用 Babel 和 webpack 转译 JavaScript 文件。

#### sass-loader
转化sass为css文件，并且包一层module.exports成为一个js module。

#### css-loader
则处理其中的@import和url()

#### url-loader
功能类似于 file-loader，但是在文件大小（单位 byte）低于指定的限制时，可以返回一个 DataURL。

#### style-loader
将创建一个style标签将css文件嵌入到html中。

#### cache-loader
在一些性能开销较大的 loader 之前添加此 loader，以将结果缓存到磁盘里。

#### file-loader
将一个文件中的 import/require() 解析为 url，并且将文件发送到输出文件夹。分发文件到output目录并返回相对路径

#### ts-loader
将ts转为js，再使用babel将js转为低版本js

```js
const loaderUtils = require('loader-utils');

module.exports = function (source) {
  let loaderOptions = loaderUtils.getOptions(source) || {}; // 获取当前loader传入的options
  return source;
}

```