# The-front-end-code-specification

###css规范

- 涉及js影响的css类以 j 开头， 不带任何样式
- 命名语意化，全部小写
- 全局通用类放在 global css 样式以 以g开头
- 两个空格代替制表符
- 为选择器分组时，将单独的选择器单独放在一行
- 对于属性值或颜色参数，省略小于 1 的小数前面的 0 （例如，.5 代替 0.5；-.5px 代替 -0.5px）
- 十六进制值应该全部小写，例如，#fff。在扫描文档时，小写字符易于分辨，因为他们的形式更易于区分
- 避免为 0 值指定单位，例如，用 margin: 0; 代替 margin: 0px;
- 相关的属性声明 －－ sublime 插件格式化
- 简写形式的属性声明
- 良好的注释
- css编码风格 sublime cssformat
- 尽量少的重绘和重排，当需要给元素设置样式时，超过2个及2个以上时，采用className处理
- CSS级联深度不能超过4层

####class 命名

- class 名称中只能出现小写字符和破折号 －（dashe）
- 破折号应当用于相关 class 的命名（类似于命名空间）（例如，.btn 和 .btn-danger）。
- 避免过度任意的简写。.btn 代表 button，但是 .s 不能表达任何意思。
- class 名称应当尽可能短，并且意义明确。
- 使用有意义的名称。使用有组织的或目的明确的名称，不要使用表现形式（presentational）的名称。
- 基于最近的父 class 或基本（base） class 作为新 class 的前缀。
- 使用 .js-* class 来标识行为（与样式相对），并且不要将这些 class 包含到 CSS 文件中。

####选择器

- 用元素使用 class ，避免使用 id tagName， 尽可能简短

###Javascript规范

#####变量
- 必须使用`var`关键字定义变量。

#####常量
- 使用大写字符，用下划线分隔，例如：`NAME_LIKE_THIS`；
- 推荐使用这样的常量明明模式：`<常量类型>_<适用场景>_<具体作用>`，例如：

#####分号
- 推荐使用分号，但是不作检查。

#####等值比较
- 始终使用===和!==操作符会更好。==和!=操作符会做类型强制转换。特别是，不要使用==来和"假"值做比较。

#####Latedef
- 变量声明丢在函数顶部。

#####块内函数声明
- 不能在一个块内声明一个函数。不能写成：

```javascript
if (x) {
    function foo() {}
}
```

- 如果确实需要在块中定义函数, 建议使用函数表达式来初始化变量:

```javascript
if (x) {
    var foo = function() {}
}
```

#####标准特性
- 优先使用标准特性，最大化可移植性和兼容性，尽量使用标准方法。例如优先使用`string.charAt(3)`，而不使用`string[3]`

#####没有必要分装基本类型

- 完全没必要对基础类型进行分装，有可能会引起问题：

```javascript
var x = new Boolean(false);
if (x) {
    alert('hi'); // Shows 'hi'.
}
```

- 可以用于类型转换：

```javascript
var x = Boolean(0);
if (x) {
    alert('hi'); // This will never be alerted.
}
typeof Boolean(0) == 'boolean';
typeof new Boolean(0) == 'object';
```

#####for-in迭代
- 只使用`for-in`来迭代`Object`，即所谓的`Map`或者`Hash`。用来迭代`Array`有时候会有问题：
- 使用普通的`for`循环来迭代数组：

#####关联数组
- 不允许使用关联数组，即不要把`Array`当作`Object`来使用。

#####多行字符串
- 不允许像下面这边书写多行字符串，非`ECMAScript`规范：
```javascript
var myString = 'A rather long string of English text, an error message \
                actually that just keeps going and going -- an error 。';
```

#####内置对象原型
- 禁止扩展原生对象如： Array Math String 。

#####console & debugger
- 在提交的代码中不允许出现`console`、`debugger`。
- 开发时期的解决方案

#####dataset
- 不推荐自定义属性，推荐使用`dataset`

#####引号
- 字符串定义时推荐使用单引号`'`，关键字、保留字使用引号括起来

####编码风格

#####命名

- 常见的命名方式：`functionNamesLikeThis`, `variableNamesLikeThis`, `ClassNamesLikeThis`, `EnumNamesLikeThis`, `methodNamesLikeThis`和`SYMBOLIC_CONSTANTS_LIKE_THIS`。
- 私有的属性、变量或者方法以“`_`”开头
- 文件的命名包括小写字母、`-`、`_`（不能包含其他字符，且`-`优于`_`），使用`.js`结尾。
- 不能使用拼音。

#####推荐命名范式

- `dom`选择器调用的返回值以`$`开头，这是`jQuery`常用的方式：`$body = jQuery(document.body)`;
- `boolean`定义：比起`bEmpty`，更推荐使用`isEmpty`,`canExit`,`hasNext`这样的命名方法。推荐使用`is`、`can`、`has`这样的前缀作为这类变量的前缀。
- 函数或者方法推荐使用`动宾`或`动`结构，例如：

- 比起`arrBooks`，更推荐使用`bookList`，比起`objStates`，更推荐使用`stateMap`。
- 推荐的一些回调函数（或对象）的范式：`wordHandler`、`changeListener`、`getBookCallback`、`onLoad`。也可以使用其他能够表达功能的命名方式

#####字符串
- 单引号`'`优于双引号`"`（包含HTML的字符串）。

#####代码风格
- 使用 sublime 插件(jsformat)统一格式化

- 模块

```javascript
// 一个实用的模块
(function (global) {
    var Module = (function () {

        var data = "secret";

        return {
            // 这是一个布尔值
            bool: true,
            // 一个字符串
            string: "a string",
            // 一个数组
            array: [1, 2, 3, 4],
            // 一个对象
            object: {
                lang: "en-Us"
            },
            getData: function () {
                // 得到 `data` 的值
                return data;
            },
            setData: function (value) {
                // 返回赋值过的 `data` 的值
                return (data = value);
            }
        };
    })();

    // 其他一些将会出现在这里

    // 把你的模块变成全局对象
    global.Module = Module;

})(this);
```

- 构造器

```javascript
// 一个实用的构造器
(function (global) {

    function Ctor(foo) {

        this.foo = foo;

        return this;
    }

    Ctor.prototype.getFoo = function () {
        return this.foo;
    };

    Ctor.prototype.setFoo = function (val) {
        return (this.foo = val);
    };

    // 不使用 `new` 来调用构建函数，你可能会这样做：
    var ctor = function (foo) {
            return new Ctor(foo);
        };

    // 把我们的构建函数变成全局对象
    global.ctor = ctor;

})(this);
```

#####文件

- JavaScript程序应该作为一个 .js文件存储和发布，文件编码为`utf-8`。
- JavaScript代码不应该嵌入在HTML文件里，除非这些代码是一个单独的会话特有的或者是需要有后台开发工程师进行控制的。HTML里的JavaScript代码大大增加了页面的大小，并且很难通过缓存和压缩来缓解，同时也难以通过前端来维护。
- JavaScript文件应该在`body`里越靠后的位置越好，最好是放在最后面。这减少了由于加载`script`而导致的其它页面组件的延迟。

###编辑器配置
- 用两个空格代替制表符（soft-tab 即用空格代表 tab 符）
- 保存文件时，删除尾部的空白符
- 设置文件编码为 UTF-8
- 在文件结尾添加一个空白行


###图片
- 切图时必须合理的压缩每张图片，提高页面加载速度，如果能用1像素的就切成1像素
- 一般情况下，请保存为 `png-8` 格式，所有能保存为静态gif的图像，都应该保存为 png-8 格式
- png-24与jpg都是一种压缩图像格式，但是与jpg不同，`png-24` 是无损压缩，因此不会降低图像的品质（比如jpg图像锐利边缘的噪点），这也是要求效果图使用`png-24`格式保存的原因。
- jpg就不多说了。jpg作为一种有损压缩格式，在每次使用它压缩的时候，均会再次降低图像的品质。多次编辑同一个jpg图像，情况会变得越来越糟糕。所以一定要从设计师手中拿到无损格式的设计稿再进行工作。一般不应该为JPG格式，除非这个图像：色值远超过256色(鲜艳而华丽)，保存为索引颜色会出现明显的梯度变化（梯田），颜色抖动（点状渐变）
- 一般css背景图不使用 jpg 格式的图像

###构建工具 and 开发环境
- Gulp
- Sublime
- NodeJs
- Nginx
- Chrome

####Sublime Package

- jsformat js
- jQuery js提示插件
- Css format css格式化
- Csscomb css属性格式化排序

> 包配置文件(需翻墙):[Preferences.sublime-settings](https://gist.github.com/RaymondYe/6a40e34a49e36fcced09)
> Sublime配置文件(需翻墙):[Package Control.sublime-settings](https://gist.github.com/RaymondYe/094985865060b94a6f63)

####Gulp

- [Gulp官网](http://gulpjs.com/)
- gulp.spritesmith  css sprite插件

####NodeJs
> [NodeJs](http://nodejs.org/)


###Reference

1.[Bootstrap 编码规范](http://codeguide.bootcss.com/)
2.[NEC 编码规范](http://nec.netease.com/standard)
3.[Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)

