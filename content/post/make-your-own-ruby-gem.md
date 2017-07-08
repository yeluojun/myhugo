---
title: "Make Your Own Ruby Gem"
date: 2017-05-01T13:07:39+08:00
tags: ["ruby", "gem"]
categories: ["ruby"]
---


# 创建自己的Ruby Gem

<!--more-->

## 一. Make a Gem

```
$ bundle gem ohye
Code of conduct enabled in config
      create  ohye/Gemfile
      create  ohye/lib/ohye.rb
      create  ohye/lib/ohye/version.rb
      create  ohye/ohye.gemspec
      create  ohye/Rakefile
      create  ohye/README.md
      create  ohye/bin/console
      create  ohye/bin/setup
      create  ohye/.gitignore
      create  ohye/.travis.yml
      create  ohye/CODE_OF_CONDUCT.md
Initializing git repo in /home/jun/ruby/rubystudy/ohye

```

## 二. 修改.gemspec

ohye.gemspec:

```
# coding: utf-8
lib = File.expand_path("../lib", __FILE__)
$LOAD_PATH.unshift(lib) unless $LOAD_PATH.include?(lib)
require "ohye/version"

Gem::Specification.new do |spec|
  spec.name          = "ohye"
  spec.version       = Ohye::VERSION
  spec.authors       = ["yeluojun"]
  spec.email         = ["635143970@qq.com"]

  # coding: utf-8
  lib = File.expand_path("../lib", __FILE__)
  $LOAD_PATH.unshift(lib) unless $LOAD_PATH.include?(lib)
  require "ohye/version"

  Gem::Specification.new do |spec|
    spec.name          = "ohye"
    spec.version       = Ohye::VERSION
    spec.authors       = ["yeluojun"]
    spec.email         = ["635143970@qq.com"]

    spec.summary       = %q{TODO: Write a short summary, because Rubygems requires one.}
    spec.description   = %q{TODO: Write a longer description or delete this line.}
    spec.homepage      = "TODO: Put your gem's website or public repo URL here."

    # Prevent pushing this gem to RubyGems.org. To allow pushes either set the 'allowed_push_host'
    # to allow pushing to a single host or delete this section to allow pushing to any host.
    if spec.respond_to?(:metadata)
      spec.metadata["allowed_push_host"] = "TODO: Set to 'http://mygemserver.com'"
    else
      raise "RubyGems 2.0 or newer is required to protect against " \
        "public gem pushes."
    end

    spec.files         = `git ls-files -z`.split("\x0").reject do |f|
      f.match(%r{^(test|spec|features)/})
    end
    spec.bindir        = "exe"
    spec.executables   = spec.files.grep(%r{^exe/}) { |f| File.basename(f) }
    spec.require_paths = ["lib"]

    spec.add_development_dependency "bundler", "~> 1.15"
    spec.add_development_dependency "rake", "~> 10.0"
    spec.add_development_dependency "rspec", "~> 3.0"
  end

  # Prevent pushing this gem to RubyGems.org. To allow pushes either set the 'allowed_push_host'
  # to allow pushing to a single host or delete this section to allow pushing to any host.
  if spec.respond_to?(:metadata)
    spec.metadata["allowed_push_host"] = "TODO: Set to 'http://mygemserver.com'"
  else
    raise "RubyGems 2.0 or newer is required to protect against " \
      "public gem pushes."
  end

  spec.files         = `git ls-files -z`.split("\x0").reject do |f|
    f.match(%r{^(test|spec|features)/})
  end
  spec.bindir        = "exe"
  spec.executables   = spec.files.grep(%r{^exe/}) { |f| File.basename(f) }
  spec.require_paths = ["lib"]

  spec.add_development_dependency "bundler", "~> 1.15"
end

```  
把 `TODO`, `FIXME`，的内容替换成自己的。  

比如:  

* `spec.summary = %q{TODO: Write a short summary, because Rubygems requires one.}`  
 替换成：  
 `spec.summary = "ruby stu gem"`  

* `spec.description   = %q{TODO: Write a longer description or delete this line.}`  
 替换成：  
 `spec.summary = "something you wan to write"`



## 二. Write code

这里新建一个文件`ohye/lib/ohye/routiao.rb`， 新建的文件必须放在`ohye/lib/ohye/`目录下:
```
module Ohye
  class Toutiao
    def say_bb
      return "bb"
    end
  end
end
```

ohye/lib/ohye.rb:
```
require "ohye/version"
require "ohye/toutiao"

module Ohye
  # Your code goes here...
  def say_hi
    return "hi!"
  end
  module_function :say_hi
end
```


ohye/lib/ohye/version.rb:
```
module Ohye
  VERSION = "0.1.0"
end

```

> __注意： 新建的文件，比如这里新建的toutiao.rb 一定要add到工作区去： `git add lib/ohye/toutiao.rb`,否则build Gem的时候会忽略该文件__

## 三. 使用 rspec 测试 你的 Gem

* 编辑 ohye.gemspec：

```
  ..
  spec.add_development_dependency "rake", "~> 10.0"
  spec.add_development_dependency "rspec", "~> 3.0"
end
```
安装所有依赖：`bundle install`

>如果bundle时间过长多半是因为墙的问题，修改 Ｇemfile 文件，将 `source "https://rubygems.org"`
替换成rubychina的源：`source "https://gems.ruby-china.org/"` 即可

* 创建spec_helper: `spec/spec_helper.rb`:

```
require "bundler/setup"
require "ohye"

RSpec.configure do |config|
  # Enable flags like --only-failures and --next-failure
  config.example_status_persistence_file_path = ".rspec_status"

  # Disable RSpec exposing methods globally on `Module` and `main`
  config.disable_monkey_patching!

  config.expect_with :rspec do |c|
    c.syntax = :expect
  end
end
```
>require "bundler/setup" 会寻找Gemfile,并引入里面的所有依赖  
 require "ohye" 引入你创建的gem

* 可以在 .rspec 文件配置一些东西：

```
--format documentation
--color
```
* 测试你的方法  

创建文件呢：`spec/ohye/toutiao_spec.rb`:  

```
require "spec_helper"

RSpec.describe 'module is Ohye:' do
  it "test toutiao" do
    qiniu = Ohye::Toutiao.new
    str = qiniu.say_bb
    expect(str). to eq("bb")
  end
end

```
运行： `rspec spec/ohye/toutiao_spec.rb`  
```
module is Ohye:
  test toutiao

Finished in 0.00393 seconds (files took 0.49788 seconds to load)
1 example, 0 failures

```  
----
## 四. 使用你的gem

Gemfile:

```
gem "ohye", github: 'yeluojun/ohye'
```

>
* 在gem项目目录内运行 `rake install` 可以直接构建并使用你的gem.
* 当gem发布后或者gem已经被使用后，gem的每一次修改都要更新版本号`VERSION`，便于`bundle update`的时候更新。
