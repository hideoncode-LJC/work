# 阻塞IO

+ 用户进程想要获取信息，调用`recvfrom`函数，进程进入阻塞状态。
+ `recvfrom`调用操作系统自带的`read`系统调用，`CPU`进入内核态。
+ 检查内核空间的`buffer`，发现暂时没有数据，不断查询。轮询、中断？
+ 数据准备就绪后，将内核空间`buffer`的数据拷贝到用户空间`buffer`中。
+ 拷贝完成，`CPU`返回用户态，开始处理数据。

![[Pasted image 20230922220448.png]]

```go
// system call
func read() {}

type user struct {} // 用户态

type kernel struct {} // 内核态

func(u *user) recvfrom() {}

func(k *kernel) 

```