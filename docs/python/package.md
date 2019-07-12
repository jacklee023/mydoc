## 1 **package**

[哪些 Python 库让你相见恨晚？【转】](https://www.cnblogs.com/jinjiangongzuoshi/p/6596268.html)
[哪些 Python 库让你相见恨晚？](https://www.zhihu.com/question/24590883)

### 1.1 **pickle**

#### 1.1.1 **dump的参数**
```
pickle.dump(obj, file, protocol=None, *, fix_imports=True)
```

pickle.dump的protocol参数可以指定序列化模式，其中0表示文本文件，1以上表示二进制文件
配合fix_imports参数可以使序列化文件可以兼容python2

### 1.2 **mccabd**

#### 1.2.1 **介绍**
   
> Cyclomatic Complexity 圈复杂度
McCabe 是一种度量程序复杂度的方法，如果单个子程序复杂度过高，或许就需要拆分逻辑提高程序的易读性。

+ [圈复杂度和McCabe](https://kinegratii.github.io/2018/04/08/cyclomatic-complexity-and-mccabe/)

#### 1.2.2 **示例**

```sh
>> pip install mccabe
>> python -m mccabe factorial.py 
>> python -m mccabe --min 5 mccabe.py
>> python -m mccabe factorial.py -d  # 产生dot有向图 
```

+ [产生dot有向图](https://dreampuf.github.io/GraphvizOnline/)

### 1.3 **Pyreverse**

#### 1.3.1 **介绍**

代码 UML 生成工具, 帮助我们理解继承关系 

#### 1.3.2 **示例**
安装成功但报错无法工作，可能是不支持python3
> TODO

### 1.4 **mypy**

#### 1.4.1 **介绍**

类型检查工具，结合 python3 的 type hint 或者 python2 中的类型注释可以做类型检查。

#### 1.4.2 **示例**

```python
mypy ./demo.py
```

#### 1.4.3 **参考**

- [mypy使用](http://blog.lujun9972.win/blog/2018/03/12/%E4%BD%BF%E7%94%A8mypy%E5%AF%B9python%E7%A8%8B%E5%BA%8F%E8%BF%9B%E8%A1%8C%E9%9D%99%E6%80%81%E6%A3%80%E6%9F%A5/)

### 1.5 **Clonedigger**

#### 1.5.1 **介绍**

重复代码 
```sh
git clone https://github.com/jlachowski/clonedigger
cd clonedigger
python setup.py install
```

#### 1.5.2 **示例**


> TODO

#### 1.5.3 **参考**

[python ddt数据驱动（简化重复代码）](https://www.cnblogs.com/shenh/p/10412685.html)

### 1.6 **urwid**

#### 1.6.1 **介绍**

urwid 不支持windows（fcntl无法安装），据说比较传统，感觉上跟QT比较像

#### 1.6.2 **参考**

- [浅谈用urwid库实现终端的GUI编程](https://agave233.github.io/2018/03/11/%E6%B5%85%E8%B0%88%E7%94%A8urwid%E5%BA%93%E5%AE%9E%E7%8E%B0%E7%BB%88%E7%AB%AF%E7%9A%84GUI%E7%BC%96%E7%A8%8B/)
- [urwid官网](http://urwid.org/index.html)

### 1.7 **npyscreen**

#### 1.7.1 **介绍**

依赖curses库，该库在Windows下需要用whl按照，但官网提供的whl包没有python34版，无法解决

### 1.8 **cPickle**

### 1.9 **pipe**