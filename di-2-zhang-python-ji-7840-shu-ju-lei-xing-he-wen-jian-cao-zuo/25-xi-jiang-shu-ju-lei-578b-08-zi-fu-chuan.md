## 定义

字符串是一个有序的字符的集合，用于存储和表示基本的文本信息，’ ‘或’’ ‘’或’’’ ‘’’中间包含的内容称之为字符串

**创建：**

```
 s = 'Hello,Eva！How are you?'
```

## 特性：

1. 按照从左到右的顺序定义字符集合，下标从0开始顺序访问，有序

2. ![](https://book.apeland.cn/media/images/2019/03/03/str.png)

3. 可以进行切片操作

4. 不可变，字符串是不可变的，不能像列表一样修改其中某个元素，所有对字符串的修改操作其实都是相当于生成了一份新数据。



补充：

1.字符串的单引号和双引号都无法取消特殊字符的含义，如果想让引号内所有字符均取消特殊意义，在引号前面加r，如name＝r’l\thf’

## 字符串的常用操作

字符串操作方法有非常多，但有些不常用 ，我们只讲重要的一些给大家，其它100年都用不上的有兴趣可以自己研究

![](https://book.apeland.cn/media/images/2019/03/03/image.png)

```py
def capitalize(self):  
    首字母大写
def casefold(self):  
    把字符串全变小写
    >> > c = 'Alex Li'
    >> > c.casefold()
    'alex li'
def center(self, width, fillchar=None):  
    >> > c.center(50, "-")
    '---------------------Alex Li----------------------'
def count(self, sub, start=None, end=None):  
    """
    S.count(sub[, start[, end]]) -> int
    >>> s = "welcome to apeland"
    >>> s.count('e')
    3
    >>> s.count('e',3)
    2
    >>> s.count('e',3,-1)
    2
def encode(self, encoding='utf-8', errors='strict'):  
    """
    编码，日后讲
def endswith(self, suffix, start=None, end=None):
    >> > s = "welcome to apeland"
    >> > s.endswith("land") 判断以什么结尾
    True
def find(self, sub, start=None, end=None):  
    """
    S.find(sub[, start[, end]]) -> int
    Return the lowest index in S where substring sub is found,
    such that sub is contained within S[start:end].  Optional
    arguments start and end are interpreted as in slice notation.
    Return -1 on failure.
    """
    return 0
def format(self, *args, **kwargs):  # known special case of str.format
    >> > s = "Welcome {0} to Apeland,you are No.{1} user."
    >> > s.format("Eva", 9999)
    'Welcome Eva to Apeland,you are No.9999 user.'
    >> > s1 = "Welcome {name} to Apeland,you are No.{user_num} user."
    >> > s1.format(name="Alex", user_num=999)
    'Welcome Alex to Apeland,you are No.999 user.'
def format_map(self, mapping):  
    """
    S.format_map(mapping) -> str
    Return a formatted version of S, using substitutions from mapping.
    The substitutions are identified by braces ('{' and '}').
    """
    讲完dict再讲这个
def index(self, sub, start=None, end=None):  
    """
    S.index(sub[, start[, end]]) -> int
    Return the lowest index in S where substring sub is found, 
    such that sub is contained within S[start:end].  Optional
    arguments start and end are interpreted as in slice notation.
    Raises ValueError when the substring is not found.
    """
def isdigit(self):  
    """
    S.isdigit() -> bool
    Return True if all characters in S are digits
    and there is at least one character in S, False otherwise.
    """
    return False
def islower(self):  
    """
    S.islower() -> bool
    Return True if all cased characters in S are lowercase and there is
    at least one cased character in S, False otherwise.
    """
def isspace(self):  
    """
    S.isspace() -> bool
    Return True if all characters in S are whitespace
    and there is at least one character in S, False otherwise.
    """
def isupper(self):  
    """
    S.isupper() -> bool
    Return True if all cased characters in S are uppercase and there is
    at least one cased character in S, False otherwise.
    """
def join(self, iterable):  
    """
    S.join(iterable) -> str
    Return a string which is the concatenation of the strings in the
    iterable.  The separator between elements is S.
    """
    >>> n = ['alex','jack','rain']
    >>> '|'.join(n)
    'alex|jack|rain'
def ljust(self, width, fillchar=None):  
    """
    S.ljust(width[, fillchar]) -> str
    Return S left-justified in a Unicode string of length width. Padding is
    done using the specified fill character (default is a space).
    """
    return ""
def lower(self):  
    """
    S.lower() -> str
    Return a copy of the string S converted to lowercase.
    """
    return ""
def lstrip(self, chars=None):  
    """
    S.lstrip([chars]) -> str
    Return a copy of the string S with leading whitespace removed.
    If chars is given and not None, remove characters in chars instead.
    """
    return ""
def replace(self, old, new, count=None):  
    """
    S.replace(old, new[, count]) -> str
    Return a copy of S with all occurrences of substring
    old replaced by new.  If the optional argument count is
    given, only the first count occurrences are replaced.
    """
    return ""
def rjust(self, width, fillchar=None):  
    """
    S.rjust(width[, fillchar]) -> str
    Return S right-justified in a string of length width. Padding is
    done using the specified fill character (default is a space).
    """
    return ""
def rsplit(self, sep=None, maxsplit=-1):  
    """
    S.rsplit(sep=None, maxsplit=-1) -> list of strings
    Return a list of the words in S, using sep as the
    delimiter string, starting at the end of the string and
    working to the front.  If maxsplit is given, at most maxsplit
    splits are done. If sep is not specified, any whitespace string
    is a separator.
    """
    return []
def rstrip(self, chars=None):  
    """
    S.rstrip([chars]) -> str
    Return a copy of the string S with trailing whitespace removed.
    If chars is given and not None, remove characters in chars instead.
    """
    return ""
def split(self, sep=None, maxsplit=-1):  
    """
    S.split(sep=None, maxsplit=-1) -> list of strings
    Return a list of the words in S, using sep as the
    delimiter string.  If maxsplit is given, at most maxsplit
    splits are done. If sep is not specified or is None, any
    whitespace string is a separator and empty strings are
    removed from the result.
    """
    return []
def startswith(self, prefix, start=None, end=None):  
    """
    S.startswith(prefix[, start[, end]]) -> bool
    Return True if S starts with the specified prefix, False otherwise.
    With optional start, test S beginning at that position.
    With optional end, stop comparing S at that position.
    prefix can also be a tuple of strings to try.
    """
    return False
def strip(self, chars=None):  
    """
    S.strip([chars]) -> str
    Return a copy of the string S with leading and trailing
    whitespace removed.
    If chars is given and not None, remove characters in chars instead.
    """
    return ""
def swapcase(self):  
    """
    S.swapcase() -> str
    Return a copy of S with uppercase characters converted to lowercase
    and vice versa.
    """
    return ""
def upper(self):  
    """
    S.upper() -> str
    Return a copy of S converted to uppercase.
    """
    return ""
def zfill(self, width):  
    """
    S.zfill(width) -> str
    Pad a numeric string S with zeros on the left, to fill a field
    of the specified width. The string S is never truncated.
    """
    return ""
```



