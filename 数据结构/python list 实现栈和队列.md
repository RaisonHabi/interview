## 一、list实现栈
直接使用list的append和pop方法
```
#定义一个空 list 当做栈
stack = []
stack.append(1)
stack.append(2)
stack.append("hello")
print(stack)
print("取一个元素：",stack.pop())
print("取一个元素：",stack.pop())
print("取一个元素：",stack.pop())
```
输出结果为：
```
[1, 2, 'hello']
取一个元素： hello
取一个元素： 2
取一个元素： 1
```

&nbsp;
## 二、list实现队列
### 1.使用append和pop(0)
```
queue=[]
queue.append(1)
queue.append(2)
queue.append('hello')
print(queue)
print("取一个元素：",queue.pop(0))
print("取一个元素：",queue.pop(0))
print("取一个元素：",queue.pop(0))
```
运行结果为：
```
[1, 2, 'hello']
取一个元素： 1
取一个元素： 2
取一个元素： hello
```
### 2.使用insert（0，）和pop()
```
#定义一个空列表，当做队列
queue = []
#向列表中插入元素
queue.insert(0,1)
queue.insert(0,2)
queue.insert(0,"hello")
print(queue)
print("取一个元素：",queue.pop())
print("取一个元素：",queue.pop())
print("取一个元素：",queue.pop())
```
运行结果为：
```
['hello', 2, 1]
取一个元素： 1
取一个元素： 2
取一个元素： hello
```

&nbsp;
## 三、collections模块实现栈和队列
前面使用 list 实现队列的例子中：
```
插入数据的部分是通过 insert() 方法实现的，这种方法效率并不高，因为每次从列表的开头插入一个数据，列表中所有元素都得向后移动一个位置;

列表在末端进行append和pop时效率很高，但是在首端pop很慢（因为移动队首元素需要将后面的元素各移动一位）。
```

这里介绍一个相对更高效的方法，即使用标准库的 **collections 模块中的 deque 结构体，它被设计成在两端存入和读取都很快的特殊 list，可以用来实现栈和队列的功能**。

从上面的图可以看出，**用list直接实现队列和用collections.deque实现在10万级别的数据上有接近100倍的差距**。
```
queueAndStack = deque()
queueAndStack.append(1)
queueAndStack.append(2)
queueAndStack.append("hello")
print(list(queueAndStack))

#实现队列功能，从队列中取一个元素，根据先进先出原则，这里应输出 1
print(queueAndStack.popleft())

#实现栈功能，从栈里取一个元素，根据后进先出原则，这里应输出 hello
print(queueAndStack.pop())
#再次打印列表
print(list(queueAndStack))
```
输出结果为：
```
[1, 2, 'hello']
1
hello
[2]
```

&nbsp;
## reference
[Python list列表实现栈和队列](http://c.biancheng.net/view/5771.html)   
[Python——用列表实现栈和队列](https://www.jianshu.com/p/bb509821c373)
