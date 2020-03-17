#### 输出流和输入流

这里的输入输出流，都是针对程序本身。程序打算输出到外面的，不管是输出到文件还是显示器。
而输入就是要读入到程序中的，从外部文件或者标准输入读取。
所以对程序来说，针对输出流一般进行写操作，针对输入流一般进行读操作。

#### stringstream ss(" mds_load is ")之后通过operator<<之后为什么没有输出

其实是原有的数据被operator<<操作覆盖掉。stringstream继承iostream，所有的ostream都有一个位置属性。
有对应的接口tellp()可以查看位置。在ss初始化之后，write的位置并没有改变，所以<<操作会覆盖原有数据。
当<<之后再去看这个值就发现已经改变，所以<<是在追加。如果要让初始化的数据不会被覆盖，那么需要通过seekp来设置位置。
对应的，对于输入流，有tellg()和seekg()接口。

#### stringstream 字符串流中的clear() 接口并不会清空原有数据

ss.clear() 不会清空流内容，只会设置错误标记，如果要清空内容，请用ss.str("")

#### map

中判断一个key是否存在用count函数
```
std::map<int, int> level_to_expire;
level_to_expire.count(k);
```

#### string

* 中的substr接口用来获取子串
* string中的find接口如果找到的字串在开头那么会返回0
所以不能通过 if (str.find("pattern"))来判断能找到，而要通过 if (string::npos != str.find("pattern")) 来进行。
