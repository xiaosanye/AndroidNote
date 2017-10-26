## AttributeSet atts;
## atts.getAttributeIntValue()

经常使用getAttributeIntValue（）方法，但是大多使用的形式是attrs.getAttributeFloatValue(null, "xxx", 0);只是在中间传一个字符串，来获取属性值

今天突然看到某程序的源码中，三个参数都传入了值。网上找attrs.getAttributeFloatValue方法的详解，结果都不是很满意。从android源码中找到如下信息。

 正文，具体的使用场景就不多说了，主要说该方法的参数解析

 getAttributeIntValue（）--通常--需要传入3个参数，分别是
 String `namespace`, String `attribute`, int `defaultValue`

   + namespace是命名空间。

   + attribute是在布局文件中所写的属性

   + defaultvalue是当通过getAttributeIntValue（）去查找时，没有找到相应的值，值默认返回defaultvalue。






























































#
