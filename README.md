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
- 使用变量