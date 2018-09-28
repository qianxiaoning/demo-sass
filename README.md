#### 安装ruby
- window下安装ruby，勾选Add Ruby executables to your PATH
- ruby -v 检测
- 换gem源。
> //1.删除原gem源
gem sources --remove https://rubygems.org/

//2.添加国内淘宝源
gem sources -a https://ruby.taobao.org/

//3.打印是否替换成功
gem sources -l

//4.更换成功后打印如下
*** CURRENT SOURCES ***
https://ruby.taobao.org/

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