---
title: "Get Started With Ruby Rake"
date: 2017-06-06T15:06:35+08:00
tags: ["Ruby", "rake"]
categories: ["Ruby"]
---


## 一. 创建任务
准备工作：先创建一个叫rake的文件夹，创建一个叫Ｒakefile的文件；然后在rake文件夹里面创建一个叫tasks的文件夹，
然后在rake文件夹里面创建一个叫hello.rake文件

<!--more-->

Rakefile:

```
import "tasks/hello.rake"

desc "example_one"
task :example_one do
    puts 'this is task one'
end

```

hello.rake:

```
task :example_two do
    puts 'this is task two'
end

```

在Ｒakefile所在的目录来执行这些任务：
```
$ rake example_one
$ rake example_two

```

输出的的结果是：

"this is task one"

"this is task two"

> 为什么Rakefile引入tasks/hello.rake要用import不用require呢？
这是因为，"require" 只能识别".rb"结尾的文件，找不到.rake结尾的文件，会报“no such file to load”异常。
当然，我们也可以直接在Rakefile文件上写自己的任务。

## 二. 创建有依赖关系的任务

```
task :base_example do
  puts 'this is base example'
end

task other_example: :base_example do
  puts 'this is other example'
end

task another_example: :other_example do
  puts 'this is another example'
end
```

我们来跑一下：

```
$rake base_example

"this is base example"


$rake other_example

"this is base example"

"this is other example"


$rake another_example

"this is base example"

"this is other example"

"this is another example"

```

> 当一个任务依赖另一个任务时，它总是要先等待上一个任务完成才执行

## 三. 命名空间

顾名思义要用到namespace了

```
namespace :article do
  desc 'create a article'  # 任务的描述
  task :create_article do
    puts 'create an article'
  end
end

```


>"desc" 是任务的描述，我们写了desc的时候运行 rake -T 会显示出我们描述过的任务，那些没有被描述的任务则不会显示，不管怎么说，习惯性的描述一下总是对的：

```
$rake -T
rake example_one                                        # example_one
rake article: create_article                            # create a article

```

运行article命名空间下的一个任务：
```
$ rake article:create_article
"create an article"
```

> 常使用命名空间给任务分组，便于管理，也能减少命名冲突等问题，当然看起开也优雅一些

## 四. 任务的参数传递

```
desc "my info"
task :my_personal_info, [:name, :sex, :age] do |t, args|
  puts "my name is #{args.name}, sex is #{args.sex}, age is #{args.age}"
end

desc "my other info"
task :my_personal_other_info, [:weight, height] do |t,args|
  task(:my_personal_info).invoke(:yeluojun, :male, 25)  # 依赖的另一种写法，invoke可以换成execute
  puts "my weight is #{args.weight} and height is #{args.height}"
end
```

跑一下：

```
$rake my_personal_info[yeluojun,male,25]
"my name is yeluojun, sex is male, age is 25"

$rake my_personal_other_info[60, 170]
"my name is yeluojun, sex is male, age is 25"
"my weight is 60 and height is 170"
```

## 五. 在 rails 中使用 rake

如果需要引用Rails环境需要引入environment比如：

```
desc "test one"
task task_one: :environment do
  puts: "task one"
end
```
rails的默认环境为 development，可以通过 RAILS_ENV 参数来修改，

```
$rake task_one RAILS_ENV = test  # 用测试环境跑task
$rake task_one RAILS_ENV = production  # 用生产环境跑task
```

__注意: rake 文件应放在 lib/tasks目录，如 lib/tasks/one.rake__


<!--more-->
