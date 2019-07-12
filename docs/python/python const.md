### 3.1 **python常量**

#### 3.1.1 **True**

#### 3.1.2 **False**

#### 3.1.3 **None**

#### 3.1.4 **NotImplemented**

> NotImplemented多用于一些二元特殊方法(比如`__eq__`、`__lt__`等)中做为返回值，表明没有实现方法，而Python在结果返回NotImplemented时会聪明的交换二个参数进行另外的尝试。

#### 3.1.5 **Ellipsis/...**
> Ellipsis是ellipsis类型的常量，它和…是等价的，bool为真

从Python 3开始，省略号本质上是另一个类似于None的单例常数，但没有特定的预期用途。 现有用途包括：

+ 在切片语法中表示剩余维度中的完整切片
+ 在类型提示中仅表示某种类型的一部分（`None`或`Tuple[str, ...]`）
+ 在类型存根文件中，指示存在默认值而未指定它

可能的用途包括：

+ 作为None是有效选项的地方的默认值
+ 作为函数的内容，您还没有实现

我的理解

+ 用作占位符，配合`__getitem__`方法实现有趣的功能
+ 代替pass用来搞事

#### 3.1.6 **__debug__**

>  如果Python没有使用-O选项启动，此常量是真值，否则是假值。

简单形式 assert expression 等价于
```python
if __debug__:
    if not expression: raise AssertionError
```
扩展形式 assert expression1, expression2 等价于
```python
if __debug__:
    if not expression1: raise AssertionError(expression2)
```

#### 3.1.7 **参考**

[python常量](https://www.cnblogs.com/sesshoumaru/p/python-constants.html)

[Python Ellipsis对象有什么作用？](https://www.itranslater.com/qa/details/2107256373464531968)

[Python 的 Ellipsis 对象](https://farer.org/2017/11/29/python-ellipsis-object/)

[Python 装逼篇之 Ellipsis](https://www.keakon.net/2014/12/05/Python%E8%A3%85%E9%80%BC%E7%AF%87%E4%B9%8BEllipsis)