### 引入脚本位置  
由于脚本会阻塞页面其他资源的下载，因此推荐将所有`<script>`标签尽可能放到`<body>`标签的底部，以尽量减少对整个页面下载的影响

### 何时用单引号，何时用双引号  
虽然在JavaScript当中，双引号和单引号都可以表示字符串, 为了避免混乱，我们建议在HTML中使用双引号，在JavaScript中使用单引号，但为了兼容各个浏览器，也为了解析时不会出错，定义JSON对象时，最好使用双引号。

### 类型转换  
```javascript
var myVar = '3.14159',
    str = '' + myVar, //  to string  ==> '3.14159'
    i_int = ~ ~myVar,  //  to integer  ==> 3
    f_float = 1 * myVar,  //  to float  ==> 3.14159
    strToNum = +myVar,  // to number ==> 3.14159
    b_bool = !!myVar,  //  to boolean - any string with length and any number except 0 are true  ==> true
    array = [myVar];  //  to array ==> ['3.14159']
```

### 使用+号时需谨慎
JavaScript 和其他编程语言不同的是，在 JavaScript 中，’+'除了表示数字值相加，字符串相连接以外，还可以作一元运算符用，把字符串转换为数字。因而如果使用不当，则可能与自增符’++’混淆而引起计算错误
```javascript
var valueA = 20, valueB = '10';
alert(valueA + valueB);     //ouput: 2010 
alert(valueA + (+valueB));  //output: 30 
alert(valueA + +valueB);    //output:30 
alert(valueA ++ valueB);     //Compile error
```

### 多个类型声明  
在JavaScript中所有变量都可以使用单个var语句来声明，这样就是组合在一起的语句，以减少整个脚本的执行时间，就如上面代码一样。 

### 使用直接量创建对象   
```
var aTest = new Array(); //替换为
var aTest = [];
var aTest = new Object; //替换为
var aTest = {};
var reg = new RegExp(); //替换为
var reg = /../;
//如果要创建具有一些特性的一般对象，也可以使用字面量，如下：
var oFruit = new O;
oFruit.color = 'red';
oFruit.name = 'apple';
//前面的代码可用对象字面量来改写成这样： 
var oFruit = { color: "red", name: "apple" };
```

### 字符串连接  
如果要连接多个字符串，应该少使用+=，如
```
s+=a;
s+=b;
s+=c;

//应该写成:
s+=a + b + c;  
```
而如果是收集字符串，比如多次对同一个字符串进行+=操作的话，最好使用一个缓存，使用JavaScript数组来收集，最后使用join方法连接起来。

### 释放javascript对象  
在rich应用中，随着实例化对象数量的增加，内存消耗会越来越大。所以应当及时释放对对象的引用，让GC能够回收这些内存控件。  
释放对象：obj = null  
释放对象属性：delete obj.myproperty  
释放数组item：使用数组的splice方法释放数组中不用的item  
