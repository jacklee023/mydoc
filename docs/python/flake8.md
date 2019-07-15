## flake8

### 插件

安装[flake8插件](https://github.com/DmytroLitvinov/awesome-flake8-extensions)

### [PEP8-Naming](https://github.com/PyCQA/pep8-naming)

#### introduce

#### install

`pip install pep8-naming`

#### erc code

| code | message                                               |
|------|-------------------------------------------------------|
| N801 | class names should use CapWords convention            |
| N802 | function name should be lowercase                     |
| N803 | argument name should be lowercase                     |
| N804 | first argument of a classmethod should be named 'cls' |
| N805 | first argument of a method should be named 'self'     |
| N806 | variable in function should be lowercase              |
| N807 | function name should not start and end with '__'      |
| N811 | constant imported as non constant                     |
| N812 | lowercase imported as non lowercase                   |
| N813 | camelcase imported as lowercase                       |
| N814 | camelcase imported as constant                        |
| N815 | mixedCase variable in class scope                     |
| N816 | mixedCase variable in global scope                    |

#### Options

The following flake8 options are added:
--ignore-names              Ignore errors for specific variable names.

                            Currently, this option can only be used for N802, N803, N806, N815, and N816 errors.

                            Default: ``setUp,tearDown,setUpClass,tearDownClass,setUpTestData,failureException,longMessage,maxDiff``.

--classmethod-decorators    List of method decorators pep8-naming plugin should consider class method.

                            Used to prevent false N804 errors.

                            Default: ``classmethod``.

--staticmethod-decorators   List of method decorators pep8-naming plugin should consider static method.

                            Used to prevent false N805 errors.

                            Default: ``staticmethod``.

### [flake8-fixme](https://github.com/tommilligan/flake8-fixme) 

#### introduce

发现fixme等关键字 要求python3.6+

#### install

`pip install flake8-fixme`

#### erc code

code | message
-----|---------------------
T100 | line contains FIXME
T101 | line contains TODO
T102 | line contains XXX

### [flake8-eradicate](https://github.com/sobolevn/flake8-eradicate) 

#### introduce

发现废弃代码 要求python3.6+ 

#### install

`pip install flake8-eradicate`

#### erc code

code | Description
-----|---------------------
E800 | Found commented out code

#### Options

--eradicate-aggressive to enable aggressive mode from eradicate, can lead to false positives

### [flake8-broken-line](https://github.com/sobolevn/flake8-broken-line)

要求python3.6+

#### install

`pip install flake8-broken-line`

#### erc code

code | Description
-----|---------------------
N400 | Found backslash that is used for line breaking

### [flake8-commas](https://github.com/PyCQA/flake8-commas)

#### introduce

逗号`,`使用不正确

#### install

`pip install flake8-commas`

#### erc code

Code | message
-----|---------------------
C812 | missing trailing comma
C813 | missing trailing comma in Python 3
C814 | missing trailing comma in Python 2
C815 | missing trailing comma in Python 3.5+
C816 | missing trailing comma in Python 3.6+
C818 | trailing comma on bare tuple prohibited
C819 | trailing comma prohibited

### [flake8-builtins](https://github.com/gforcada/flake8-builtins)
#### introduce
内部类型被用作变量或参数
#### install
`pip install flake8-builtins`
#### erc code

TODO

### [flake8-comprehensions](https://github.com/adamchainz/flake8-comprehensions)
#### introduce
不必要的迭代器等
#### install
`pip install flake8-comprehensions`
#### erc code

Code | message
-----|---------------------
C400 | Unnecessary generator - rewrite as a list comprehension.
C401 | Unnecessary generator - rewrite as a set comprehension.
C402 | Unnecessary generator - rewrite as a dict comprehension.
C403 | Unnecessary list comprehension - rewrite as a set comprehension.
C404 | Unnecessary list comprehension - rewrite as a dict comprehension.
C405 | Unnecessary (list/tuple) literal - rewrite as a set literal.
C406 | Unnecessary (list/tuple) literal - rewrite as a dict literal.
C407 | Unnecessary list comprehension - '<builtin>' can take a generator.
C408 | Unnecessary (dict/list/tuple) call - rewrite as a literal.
C409 | Unnecessary (list/tuple) passed to tuple() - (remove the outer call to tuple()/rewrite as a tuple literal).
C410 | Unnecessary (list/tuple) passed to list() - (remove the outer call to list()/rewrite as a list literal).
C411 | Unnecessary list call - remove the outer call to list().

### [flake8-bugbear](https://github.com/PyCQA/flake8-bugbear)
#### introduce
不明觉厉
#### install
`pip install flake8-bugbear`
#### erc code
Code | message
-----|---------------------
**B001** | Do not use bare ``except:``, it also catches unexpected events like memory errors, interrupts, system exit, and so on.  Prefer ``except Exception:``.  If you're sure what you're doing, be explicit and write ``except BaseException:``.  Disable E722 to avoid duplicate warnings.
**B002** | Python does not support the unary prefix increment. Writing ``++n`` is equivalent to ``+(+(n))``, which equals ``n``. You meant ``n += 1``.
**B003** | Assigning to ``os.environ`` doesn't clear the environment.  Subprocesses are going to see outdated variables, in disagreement with the current process.  Use ``os.environ.clear()`` or the ``env=``  argument to Popen.
**B004** | Using ``hasattr(x, '__call__')`` to test if ``x`` is callable is unreliable.  If ``x`` implements custom ``__getattr__`` or its ``__call__`` is itself not callable, you might get misleading results.  Use ``callable(x)`` for consistent results.
**B005** | Using ``.strip()`` with multi-character strings is misleading the reader. It looks like stripping a substring. Move your character set to a constant if this is deliberate. Use ``.replace()`` or regular expressions to remove string fragments.
**B006** | Do not use mutable data structures for argument defaults.  All calls reuse one instance of that data structure, persisting changes between them.
**B007** | Loop control variable not used within the loop body.  If this is intended, start the name with an underscore.
**B008** | Do not perform calls in argument defaults.  The call is performed only once at function definition time.  All calls to your function will reuse the result of that definition-time call.  If this is intended, assign the function call to a module-level variable and use that variable as a default value.
**B009** | Do not call ``getattr(x, 'attr')``, instead use normal property access: ``x.attr``. Missing a default to ``getattr`` will cause an ``AttributeError`` to be raised for non-existent properties. There is no additional safety in using ``getattr`` if you know the attribute name ahead of time.
**B010** | Do not call ``setattr(x, 'attr', val)``, instead use normal property access: ``x.attr = val``. There is no additional safety in using ``setattr`` if you know the attribute name ahead of time.
**B011** | Do not call `assert False` since `python -O` removes these calls. Instead callers should `raise AssertionError()`.
**B301** | Python 3 does not include ``.iter*`` methods on dictionaries. The default behavior is to return iterables. Simply remove the ``iter`` prefix from the method.  For Python 2 compatibility, also prefer the Python 3 equivalent if you expect that the size of the dict to be small and bounded. The performance regression on Python 2 will be negligible and the code is going to be the clearest.  Alternatively, use ``six.iter*`` or ``future.utils.iter*``. 
**B302** | Python 3 does not include ``.view*`` methods on dictionaries. The default behavior is to return viewables. Simply remove the ``view`` prefix from the method.  For Python 2 compatibility, also prefer the Python 3 equivalent if you expect that the size of the dict to be small and bounded. The performance regression on Python 2 will be negligible and the code is going to be the clearest.  Alternatively, use ``six.view*`` or ``future.utils.view*``. 
**B303** | The ``__metaclass__`` attribute on a class definition does nothing on Python 3. Use ``class MyClass(BaseClass, metaclass=...)``. For Python 2 compatibility, use ``six.add_metaclass``. 
**B304** | ``sys.maxint`` is not a thing on Python 3. Use ``sys.maxsize``. 
**B305** | ``.next()`` is not a thing on Python 3. Use the ``next()`` builtin. For Python 2 compatibility, use ``six.next()``. 
**B306** | ``BaseException.message`` has been deprecated as of Python 2.6 and is removed in Python 3. Use ``str(e)`` to access the user-readable message. Use ``e.args`` to access arguments passed to the exception. 
**B901** | Using ``return x`` in a generator function used to be syntactically invalid in Python 2. In Python 3 ``return x`` can be used in a generator as a return value in conjunction with ``yield from``. Users coming from Python 2 may expect the old behavior which might lead to bugs.  Use native ``async def`` coroutines or mark intentional ``return x`` usage with ``# noqa`` on the same line. 
**B902** | Invalid first argument used for method. Use ``self`` for instance methods, and ``cls`` for class methods (which includes ``__new__`` and ``__init_subclass__``) or instance methods of metaclasses (detected as classes directly inheriting from ``type``). 
**B903** | Use ``collections.namedtuple`` (or ``typing.NamedTuple``) for data classes that only set attributes in an ``__init__`` method, and do nothing else. If the attributes should be mutable, define the attributes in ``__slots__`` to save per-instance memory and to prevent accidentally creating additional attributes on instances. 
**B950** | Line too long. This is a pragmatic equivalent of ``pycodestyle``'s E501: it considers "max-line-length" but only triggers when the value has been exceeded by **more than 10%**. You will no longer be forced to reformat code due to the closing parenthesis being one character too far to satisfy the linter. At the same time, if you do significantly violate the line length, you will receive a message that states what the actual limit is. This is inspired by Raymond Hettinger's `"Beyond PEP 8" talk <https://www.youtube.com/watch?v=wf-BqAjZb8M>`_ and highway patrol not stopping you if you drive < 5mph too fast. Disable E501 to avoid duplicate warnings.

### [flake8-spellcheck](https://github.com/MichaelAquilina/flake8-spellcheck)
#### introduce
拼写检查，允许白名单
#### install
`pip install flake8-spellcheck`
#### erc code
Code  | message
------|---------------------
SC100 | Spelling error in comments
SC200 | Spelling error in name (e.g. variable, function, class)

### [flake8-import-order](https://github.com/PyCQA/flake8-import-order)
#### introduce
导入顺序，风格可选，可以自定义风格
#### install
`pip install flake8-import-order`
#### erc code
Code | message
-----|---------------------
I100 | Your import statements are in the wrong order.
I101 | The names in your from import are in the wrong order.
I201 | Missing newline between import groups.
I202 | Additional newline in a group of imports.
#### [Styles](https://github.com/PyCQA/flake8-import-order#styles)
The following styles are directly supported,

- cryptography
- google
- smarkets
- appnexus
- edited
- pycharm
- pep8

You can also add your own style by extending Style class.

### [flake8-annotations-coverage](https://github.com/best-doctor/flake8-annotations-coverage)

#### introduce
#### install
`pip install flake8-annotations-coverage`
#### erc code

### [flake8-annotations-complexity](https://github.com/best-doctor/flake8-annotations-complexity)

#### introduce
#### install
`pip install flake8-annotations-complexity`
#### erc code

### [flake8-assertive](https://github.com/jparise/flake8-assertive)
#### introduce
检查unittest中assert语句
#### install
`pip install flake8-assertive`
#### erc code
Code | message
-----|---------------------
A500 | prefer {func} for '{op}' comparisons
A501 | prefer {func} for '{op}' expressions
A502 | prefer {func} instead of comparing to {obj}
#### configuration
- assertive-snakecase: suggest snake_case assert method names (e.g. assert_true()) instead of the standard names (e.g. assertTrue())
- assertive-test-pattern: fnmatch pattern for identifying unittest test files (and all other files will be skipped)

### [flake8-string-format](https://github.com/xZise/flake8-string-format)
#### introduce
#### install
`pip install flake8-string-format`
#### erc code

Level | message
------|---------------------
P1xx  | Presence of implicit parameters
P2xx  | Missing values in the parameters
P3xx  | Unused values in the parameters

Code | message
-----|---------------------
P101 | format string does contain unindexed parameters
P102 | docstring does contain unindexed parameters
P103 | other string does contain unindexed parameters
P201 | format call uses to large index (INDEX)
P202 | format call uses missing keyword (KEYWORD)
P203 | format call uses keyword arguments but no named entries
P204 | format call uses variable arguments but no numbered entries
P205 | format call uses implicit and explicit indexes together
P301 | format call provides unused index (INDEX)
P302 | format call provides unused keyword (KEYWORD)

### [flake8-coding](https://github.com/tk0miya/flake8-coding)
#### introduce
#### install
`pip install flake8-coding`
#### erc code
Code | message
-----|---------------------
C101 | Coding magic comment not found
| | No magic encoding comment was found in the file. As per PEP-263, this must be in the first two lines of the file.
C102 | Unknown encoding found in coding magic comment
| | The encoding found in the magic encoding comment did not match the accept-encodings option.
C103 | Coding magic comment present
| | no-accept-encodings is set, and a magic encoding comment was found in the file.

#### Options
- accept-encodings
```
[flake8]
accept-encodings = utf-8,utf-16
```
- no-accept-encodings
```
[flake8]
no-accept-encodings = True
```

### [cohesion](https://github.com/mschwager/cohesion#flake8-support)
#### introduce
内聚性检查
#### install
`pip install cohesion`
#### erc code
H601 ...
TODO

### [flake8-putty](https://github.com/jayvdb/flake8-putty)
#### introduce
智能忽略
#### install
`pip install flake8-putty`
#### erc code
TODO

### [flake8-per-file-ignores](https://github.com/snoack/flake8-per-file-ignores
#### introduce
#### install
`pip install flake8-per-file-ignores`
#### erc code
TODO

