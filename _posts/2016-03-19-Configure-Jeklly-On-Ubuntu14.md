---
layout:     post
title:      "在Ubuntu 14.04上配置Jekyll"
subtitle:   ""
---

### 安装RVM

```
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
curl -sSL https://get.rvm.io | bash （还会提示运行一个sources ....命令）
```
如果使用了Socks5代理，可能会报错（Failed to receive SOCKS5 connect request ack），可先关闭代理再试。
安装好rvm之后可以通过`rvm list known`来查看所有已知的ruby
{% highlight shell %}
$ rvm list known  
# MRI Rubies
[ruby-]1.8.6[-p420]
[ruby-]1.8.7[-head] # security released on head
[ruby-]1.9.1[-p431]
[ruby-]1.9.2[-p330]
[ruby-]1.9.3[-p551]
[ruby-]2.0.0[-p648]
[ruby-]2.1[.8]
[ruby-]2.2[.4]
[ruby-]2.3[.0]
[ruby-]2.2-head
ruby-head
...
{% endhighlight %}

### 通过RVM安装Ruby

```
$ rvm install ${version} // 如 2.1.1, 2.3
```
此命令可能会需要一段时间，期间会安装ruby所需要的依赖包。

### 安装github-pages gem
执行`gem install github-pages`
此时可能会报错说：
`ERROR:  Could not find a valid gem 'github-pages' (>= 0) in any repository`
这个时候可以通过`gem sources`查看gem源，
{% highlight shell %}
$ gem sources
*** CURRENT SOURCES ***

https://rubygems.org/
{% endhighlight %}
默认可能是https的，改成http的即可（虽然会提示“推荐使用https”，暂时没搞清楚怎么才能用上https的）。

```
gem sources --remove https://rubygems.org/
gem sources --add http://rubygems.org/
```

之后再次执行安装github-pages的命令，然后会安装一堆gems.

### 安装bundler.
执行`gem install bundler`即可。
到此为止，jekyll的配置就算结束了。