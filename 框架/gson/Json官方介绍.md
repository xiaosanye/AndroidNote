[Json官网](http://json.org/json-zh.html)

>JSON建构于两种结构：
>+ `“名称/值”对的集合（A collection of name/value pairs）`。不同的语言中，它被理解为对象（object），纪录（record），结构（struct），字典（dictionary），哈希表（hash table），有键列表（keyed list），或者关联数组 （associative array）。
>+ `值的有序列表（An ordered list of values）`。在大部分语言中，它被理解为数组（array）。

>这些都是常见的数据结构。事实上大部分现代计算机语言都以某种形式支持它们。**这使得一种数据格式在同样基于这些结构的编程语言之间交换成为可能。**

**JSON具有以下这些形式：**

1. 对象
>对象是一个无序的“‘名称/值’对”集合。一个对象以“{”（左括号）开始，“}”（右括号）结束。每个“名称”后跟一个“:”（冒号）；“‘名称/值’ 对”之间使用“,”（逗号）分隔。

![](images/json_object.gif)

2. 数组
>数组是值（value）的有序集合。一个数组以“[”（左中括号）开始，“]”（右中括号）结束。值之间使用“,”（逗号）分隔。

![](images/json_array.gif)

3. 值
>值（value）可以是双引号括起来的字符串（string）、数值(number)、true、false、 null、对象（object）或者数组（array）。这些结构可以嵌套。

![](images/json_value.gif)

4. 字符串
>字符串（string）是由双引号包围的任意数量Unicode字符的集合，使用反斜线转义。一个字符（character）即一个单独的字符串（character string）。

![](images/json_string.gif)

5. 数值
>数值（number）也与C或者Java的数值非常相似。除去未曾使用的八进制与十六进制格式。除去一些编码细节。

![](images/json_number.gif)




#
