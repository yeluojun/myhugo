---
title: "通过chanel对Go进行并发控制"
date: 2017-07-05T14:26:00+08:00
tags: ["golang", "WaitGroup", "chanel"]
categories: ["golang"]
---


## 使用chan来控制并发
直接代码：

ctl.go

```Go
package rctl
import "sync"
type Rctl struct {
	Queue chan int
	Wg    *sync.WaitGroup
}
func (r *Rctl) FuncCtl(f func(int), i int) {
	// 并发操作
	go func() {
		r.Queue <- 1  
		f(i)
		<-r.Queue
		r.Wg.Done()
	}()
}
```

ctl_test.go

```Go
package rctl
import (
	"fmt"
	"sync"
	"testing"
)
func Test_FuncCtl(t *testing.T) {
	rt := Rctl{
		Queue: make(chan int, 100), // 缓冲区为100
		Wg:    new(sync.WaitGroup),
	}
	rt.Wg.Add(400)
	for i := 100; i < 500; i++ {
		rt.FuncCtl(Af, i)
	}
	rt.Wg.Wait()
	close(rt.Queue)
}

func Af(t int) {
	fmt.Println("go to af")
	time.Sleep(time.Millisecond * time.Duration(t))
	fmt.Println(t)
}
```
此程序会在for循环那里限制最多100个并发(顺便复习了一下Ｇo的函数传递)
