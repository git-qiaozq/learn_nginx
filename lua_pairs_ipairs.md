## OpenResty学习笔记 - pairs 和 ipairs

### 官方描述
> **pairs(t)**
如果 t 有元方法 __pairs， 以 t 为参数调用它，并返回其返回的前三个值。
否则，返回三个值：next 函数， 表 t，以及 nil。 因此以下代码
for k,v in pairs(t) do body end
能迭代表 t 中的所有键值对。

> **ipairs(t)**
返回三个值（迭代函数、表 t 以及 0 ）， 如此，以下代码
for i,v in ipairs(t) do body end
将迭代键值对（1,t[1]) ，(2,t[2])， ... ，直到第一个空值。

### 不同点
**`pairs`会遍历表中所有的key-value值，而`ipairs`会根据key的数值从1开始加1递增遍历对应的table[i]值，直到出现第一个不是按1递增的数值时候退出。**

### 举例
- **遍历`pairs`**
```lua
local test_pairs = {
    [1] = 1,
    test = "test",
    ["hello"] = "hello world",
    [2] = 2,
    foo = "bar",
    "first"
}

for k, v in pairs(test_pairs) do
    print(k, v)
end
```
输出：
```
1       first
2       2
hello   hello world
test    test
foo     bar
```
解释：
遍历所有的key-value知道遇到`nil`。

- **遍历`ipairs`**
```lua
local test_pairs = {
    [1] = 1,
    test = "test",
    ["hello"] = "hello world",
    [2] = 2,
    foo = "bar",
    "first"
}

for k, v in ipairs(test_pairs) do
    print(k, v)
end
```
输出：
```
1   first
2   2
```
解释：
只有序号为`1（first）`和`2（2）`的值被输出。

### 总结
- pairs是无序的，ipairs是有序的。