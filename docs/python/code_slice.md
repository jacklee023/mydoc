
### 1 **global variable**

```python
def global_init():
    global _global_dict
    _global_dict = {}

def set_global_value(key, value):
    _global_dict[key] = value

def get_global_value(key, defVal = None):
    try:
        return _global_dict[key]
    except KeyError:
        return defVa
```
### 2 **const value**

#### 2.1 **case1**

```python
class ConstValue(object):
    class ConstError(TypeError):
        pass
    class ConstCaseError(ConstError):
        pass
    def __setter__(self, name, value):
        if self.__dict__.has_key(name):
            raise self.ConstError, 'Not allowed change const.{value}'.format(value=name)
        if not name.isupper():
            raise self.ConstCaseError, "Const's name is not all uppercase"
        self.__dict__[name] = value

#使用
ConstValue.GOOGLE = 100
```

- 参考 [Python常量的简单实现](https://www.jianshu.com/p/5ba80472385c)

#### 2.2 **case2**
```python
# const.py
class _const:
    class ConstError(TypeError): pass
    class ConstCaseError(ConstError): pass
    
    def __setattr__(self, name, value):
        if name in self.__dict__:
            raise self.ConstError("Can't change const.%s" % name)
        if not name.isupper():
            raise self.ConstCaseError("const name %s is not all uppercase" % name)
        self.__dict__[name] = value
    
import sys
sys.module[__name__] = _const()
#sys.module['const'] = _const()
```
```
# demo.py
#const = _const()
import const
const.COMPANY = 'IBM'
print(const.COMPANY)
```