### Bundle 问题部

部署的时候Gemfile 里面的source 路径总是失效的：

比如 source ```https://rubygems.org``` 换 ```https://gems.ruby-china.org``` 始终换不过来

后来的解决办法： 修改 ```~/.bundle/config```:

> ```BUNDLE_MIRROR__HTTPS://RUBYGEMS__ORG/: “https://rubygems.org”``` 的链接改掉即可，即：

> ```BUNDLE_MIRROR__HTTPS://RUBYGEMS__ORG/: “https://gems.ruby-china.org”```
