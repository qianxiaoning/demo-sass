### 快速上手
- 安装ruby 勾选Add Ruby executables to your PATH
- 安装sass gem install sass
- 纯净sass项目
```
新建.scss文件
监听多文件，scss文件夹下的scss输出到css文件夹 并按整理格式排版
sass --watch sass/:css/ --style compact
```
- compass创建sass项目
```
compass create compassSass
compass watch
在config.rb修改入口和输出路径 修改排版格式时，要重新开启watch生效
```
- 在vue中使用sass
```
1.安装sass依赖
vue init webpack demo
npm i sass-loader -D
npm i node-sass -D //sass-loader依赖node-sass
2.配置webpack
webpack.base.conf.js中的
module:{
    rules:[
        {
            test:/\.scss$/, //匹配后缀名
            loaders:['style','css','sass'] //指定loader
        }
    ]
}
3.style标签 <style lang="scss" scoped>
然后照常npm run dev即可
4.主要用语法
$btn-bgColor:blue!default; //定义变量，后面要加分号（可加默认值，使其可修改）
.page01{ //嵌套语法
    .nav{
        a{
            color:#000;
            &:hover{color:#fff;} //&代表父标签，定义hover时
        }        
    }
    .container{
        .blueBtn,.redBtn{font-size:16px;} //群组选择器
    }
    .footer{
        background{ //属性嵌套
            image:url('../..');
            color:#fff;
            repeat:no-repeat
        }
    }
}
```
---
### 安装
#### 安装ruby
- window下安装ruby，勾选Add Ruby executables to your PATH
- ruby -v 检测
- 换gem源。
```
//1.删除原gem源
gem sources --remove https://rubygems.org/

//2.添加国内淘宝源
gem sources -a https://ruby.taobao.org/

//3.打印是否替换成功
gem sources -l

//4.更换成功后打印如下
*** CURRENT SOURCES ***
https://ruby.taobao.org/
```
- 安装sass和Compass  
```
gem install sass  
gem install compass  

gem update sass //更新sass
sass -v
sass -h //查看sass帮助
```
- 命令行编译
```
//单文件转换命令
sass input.scss output.css

//单文件监听命令
sass --watch input.scss:output.css

//如果你有很多的sass文件的目录，你也可以告诉sass监听整个目录：
sass --watch app/sass:public/stylesheets
```
- 命令行编译配置选项;
```
//编译格式
sass --watch input.scss:output.css --style compact

//编译添加调试map
sass --watch input.scss:output.css --sourcemap

//选择编译格式并添加调试map
sass --watch input.scss:output.css --style expanded --sourcemap

//开启debug信息
sass --watch input.scss:output.css --debug-info

--style表示解析后的css是什么排版格式;
sass内置有四种编译格式:nested``expanded``compact``compressed。
--sourcemap表示开启sourcemap调试。开启sourcemap调试后，会生成一个后缀名为.css.map文件。

nested递进 expanded展开 compact整理 compressed压缩
我喜欢 sass style.scss:style.css --style compact
```
### 快速入门
#### 使用变量 $
- 变量声明
```
$highlight-color: #F90;
意味着变量$highlight-color现在的值是#F90
变量受限于{}规则块中

变量可以套变量
如：
$highlight-color: #F90;
$highlight-border: 1px solid $highlight-color;
.selected {
  border: $highlight-border;
}
```
- 命名方式
```
中划线 如：$highlight-color
```
#### 嵌套CSS 规则
```
#content {
  background-color: #f5f5f5;
  article {
    h1 { color: #333 }
    p { margin-bottom: 1.4em }
  }
  aside { background-color: #EEE }
}
```
#### 父选择器的标识符& &表示父元素选择器
```
如添加hover效果时
article a {
  color: blue;
  &:hover { color: red }
}
为：
article a { color: blue }
article a:hover { color: red }

另一个用法
可以在父选择器之前添加选择器

写ie的专用类
可以在父选择器之前添加选择器 加上body.ie & 
如：
#content aside {
  color: red;
  body.ie & { color: green }
}
为
#content aside {color: red};
body.ie #content aside { color: green }
```
#### 群组选择器的嵌套
```
.container h1, .container h2, .container h3 { margin-bottom: .8em }
写成：
.container {
  h1, h2, h3 {margin-bottom: .8em}
}
或者：
nav, aside {
  a {color: blue}
}
转成
nav a, aside a {color: blue} 这样
```
#### 子组合选择器和同层组合选择器：>、+和~
```
>直接子元素
+紧跟元素
~跟在后面的所有同层元素
示例：
article {
  ~ article { border-top: 1px dashed #ccc }
  > section { background: #eee }
  dl > {
    dt { color: #333 }
    dd { color: #555 }
  }
  nav + & { margin-top: 0 }
}
为：
article ~ article { border-top: 1px dashed #ccc }
article > footer { background: #eee }
article dl > dt { color: #333 }
article dl > dd { color: #555 }
nav + article { margin-top: 0 }
```
#### 嵌套属性
```
nav {
  border: {
    style: solid;
    width: 1px;
    color: #ccc;
  }
}
nav {
  border: 1px solid #ccc {
  left: 0px;
  right: 0px;
  }
}
```
#### 导入SASS文件
```
sass的@import规则在生成css文件时就把相关文件导入进来。这意味着所有相关的样式被归纳到了同一个css文件中，而无需发起额外的下载请求。

sass局部文件的文件名以下划线开头，不会在编译时单独编译，而只把这个文件用作导入
```
- 默认变量值 !default
```
$fancybox-width: 400px !default;
.fancybox {
width: $fancybox-width;
}
```
#### 嵌套导入
```
.blue-theme {@import "blue-theme"}
为
//生成的结果跟你直接在.blue-theme选择器内写_blue-theme.scss文件的内容完全一样。
.blue-theme {
  aside {
    background: blue;
    color: #fff;
  }
}
```
#### 原生的CSS导入
#### 静默注释
```
//这种注释内容不会出现在生成的css文件中
```
#### 混合器 @mixin
```
下边定义了一个非常简单的混合器，目的是添加跨浏览器的圆角边框。
@mixin rounded-corners {
  -moz-border-radius: 5px;
  -webkit-border-radius: 5px;
  border-radius: 5px;
}
使用：@include
notice {
  background-color: green;
  border: 2px solid #00aa00;
  @include rounded-corners;
}
```
#### 给混合器传参
```
如：
@mixin link-colors($normal, $hover, $visited) {
  color: $normal;
  &:hover { color: $hover; }
  &:visited { color: $visited; }
}
调用
a {
  @include link-colors(blue, red, green);
}
为：
a { color: blue; }
a:hover { color: red; }
a:visited { color: green; }

传参顺序可不一致，用$name: value的形式
a {
    @include link-colors(
      $normal: blue,
      $visited: green,
      $hover: red
  );
}
```
- 默认参数值
```
@mixin link-colors(
    $normal,
    $hover: $normal,
    $visited: $normal
  )
{
  color: $normal;
  &:hover { color: $hover; }
  &:visited { color: $visited; }
}
```
#### 使用选择器继承来精简CSS @extend
```
//通过选择器继承继承样式
.error {
  border: 1px solid red;
  background-color: #fdd;
}
.seriousError {
  @extend .error;
  border-width: 3px;
}
效果就好像是class="seriousError error"
不仅会继承.error自身的所有样式，任何跟.error有关的组合选择器样式也会被.seriousError以组合选择器的形式继承
//.seriousError从.error继承样式
.error a{  //应用到.seriousError a
  color: red;
  font-weight: 100;
}
h1.error { //应用到hl.seriousError
  font-size: 1.2rem;
}
```
- 何时使用继承
```
你发现你的某个类（比如说.seriousError）另一个类（比如说.error）的细化时使用
```
### 中文文档
- sass增加了变量 (variables)、嵌套 (nested rules)、混合 (mixins)、导入 (inline imports) 等高级功能
```
使用sass
安装 Sass
gem install sass

在命令行中运行 Sass：
sass input.scss output.css

监视单个 Sass 文件，每次修改并保存时自动编译：
sass --watch input.scss:output.css

监视整个文件夹：
sass --watch app/sass:public/stylesheets
```
#### CSS转译成SASS sass-convert
```
$ sass-convert css/style.css style.scss
```