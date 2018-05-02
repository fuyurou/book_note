# book_note
js中的函数
## 函数
函数包含一组语句，它们是js的基础模块单元，用于代码复用、信息隐藏和组合调用。函数用于指定对象的行为。
## 1.函数对象
- avaScript中的函数就是对象。对象是“名/值”对的集合并拥有一个连接到原型对象的隐藏连接。对象字面量产生的对象连接到Object.prototype。函数对象连接到Function.prototype(该原型对象本身连接到Object.prototype)。
- 每个函数对象在创建时也会有一个prototype属性。它的值是一个拥有constructor属性且值即为该函数的对象。
- 函数是对象，可以保存在变量、对象和数组中。函数可以当做参数传递给其他函数，函数也可以在返回函数，函数拥有方法。
## 2.字面量
函数对象通过函数字面量来创建：

var add = function(a,b){

return a+b;

};

 函数字面量包括四个部分：

- 1 保留字function
- 2 函数名（可省略）
- 3 包围在括号中的一组参数，在函数被调用是初始化为实际的参数的值
- 4 包围在花括号里的一组语句块

注意：一个内部函数除了可以访问自己的参数和变量，同时也可以自由的访问父函数的参数和变量。用过这种函数字面量创建的函数对象包含一个连接到外部上下文的连接。这个被称为闭包。
## 3.调用
调用一个函数会暂停当前函数的执行，传递控制权和参数给新函数。除了声明时定义的形式参数，每个函数还接收两个附加的参数：this和arguments。在JavaScript中有四种调用方式：方法调用模式，函数调用模式，构造器调用模式和apply调用模式。
- 方法调用模式

当有个函数被保存为对象的一个属性是，我们称他为一个方法。当以个方法被调用时，this被绑定到该对像。

var myObject = {
    
    value: 0,
    
    increment: function (icn) {
        
        this.value += typeof inc === 'number' ? icn: 1;
    
    }

}

myObject.increment();

console.log(myObject.value);

myObject.increment(2);

console.log(myObject.value);

方法可以使用this访问自己所属的对象。通过this可取可取的他们所属对象的上下文的方法称为公共方法
- 函数调用模式

当一个函数并非一个对象的属性时，那么它就是被当做一个函数来调用的：

var sum = add(3, 4);

以此模式调用函数，this被绑定到了全局对象。这是错误的，正确的设计应该是当内部函数被调用时，this应该绑定到外部函数的this变量。因此声明一个that变量并赋值this，内部函数就可以通过that访问到this。这个听起来比较难理解，我们以代码的形式来说明
myObject.double = function(){
    var that = this ;
    var helper = function(){
        that .value = add(that.value,that.value);
    }
    helper(); //以函数的形式调用helper
}
//以方法的形式调用double
myObject.double();
console.log(myObject.value);
- 构造器调用模式
JavaScript是基于原型继承的语言，对象可以直接从其他对象继属性，该语言是无类型的。
如果在一个函数前面带上new来调用，name背地里就会创建一个连接到该函数的prototype成员的新对象，同时this会绑定到新对象上
  //创建一个名为Quo的构造器函数，它构造一个带有status属性的对象

  var Quo=function(string){
    this.stastus=string;
  };
  //给Quo 的所有实例提供一个名为get_status 的公共方法
  Quo.prototype.get_status=function(){
      return this..status;
  };
  //构造一个Quo实例
   var myQuo =new Quo("confused");
  document.writeln(myQuo.get_status());
- Apply 调用模式
apply方法可以构建一个参数数组传递给调用函数，apply方法接收两个数组，第一个是要绑定给this的值，第二个就是一个参数数组。
  //构造一个包含两个数字的数组，并将它们相加
  var array =[3,4];
  var sum=add.apply(null,array);//sum的值为7
  //构造一个包含status成员的对象
  var statusObject={
      status:'A-OK'
  };
  //statusObject 并没有继承自Quo.prototype,但我们可以在statusObject上调用
  //用get_status方法，尽管statusObject并没有一个名为get_status的方法
  var status=Quo.prototype.get_status.apply(statusObject);
  //status的值为 'A-OK'
## 4.参数
当函数被调用时，会得到一个“免费”配送的参数，那就是argument数组
## 5.返回
一个函数总是会返回一个值。如果没有指定返回值，则返回undedined

return语句可用来是函数提前返回

如果函数调用时在前面加上了new前缀，且返回值不是一个对象，则返回this(该新对象)

## 6.异常
js提供了一套异常处理机制 throw try-catch

一个try语句只会有一个捕获所有异常的catch代码块

##7.扩充类型的功能
通过给Object.prototype添加方法，可以让该方法对所有对象都可用。这样的方式对函数、数组、字符串、数字、正则表达式和布尔值同样适用

Function.prototype.method = function(name, func) { if(!this.prototype[name]) {

    this.prototpe[name] = func;
} 
return this;
}
## 8.递归
递归函数就是会直接或间接地调用自身的一种函数

汉诺塔hanoi

var hanoi = funtion (disc, src, aux, dst) {

if(disc > 0) {

    hanoi(disc - 1, src, dst, aux);
    document.writeln('Move disc' + disc + 'from' + src + 'to' + dst);
    hanoi(disc - 1, aux, src, dst);
}
};

递归函数可以非常高效地操作树形结构 浏览器端的文档对象模型(DOM)
## 9.函数作用域
- 作用域控制着变量与参数的可见性及生命周期

js有函数作用域，在函数内部可见，函数外部不可见。内部函数可以访问定义它们的外部函数的参数和变量(除了this和argument)

var foo = funtion() {

var a = 3, b = 5;

var bar = function() {

    var b = 7, c = 11;

    a += b + c;
};
bar();
}

## 10.闭包
- 部函数可以访问定义在他们外部的函数的变量和参数（除了this、arguments）
var que = function(status){
    return {
        get_status: function(){
            return status;
        }
    }
}
var myQuo = que("hello");
console.log(myQuo.get_status());
get_status方法并不是访问参数的副本，他访问的就是参数的本身，这就是闭包，保护status为私有属性
## 11.回调
同步请求 => 假死状态

异步请求 => 回调函数 => 异步函数立即返回

request = prepare_the_request();

send_request_asynchronously(request, funtion(response) {

display(response);
})
传第一个函数作为参数给send_request_asynchronously函数，一旦接收到响应它就会被调用

## 12.模块
- 我们可以使用函数和闭包来构造模块，模块是一个提供个借口却隐藏状态与实现的函数或对象
- 模块模式利用函数作用域和闭包来创建被绑定对象与私有成员的关联
- 模块的一般形式：一个定义了私有变量和函数的函数；利用闭包创建可以访问私有变量和函数的特权，最后一个返回该特权函数，或者把它们保存在一个可以访问的到的地方
- 模块模式需要具备两个条件
1、必须有外部的封装函数，该函数必须至少被调用一次（每次调用都会创建一个新的模块实例）。
2、封闭函数必须返回至少一个尼日不函数，这样内部函数才能在私有的作用域形成闭包，并且可以访问或者可以修改私有状态。
var foo= (function(){
    var something = 'cool';
    var another =[1,2,3];
    function doSomething(){
        console.log(something);
    }
    function doAnother(){
        console.log(another.join(' ! '));
    }
    return{
        doSomething: doSomething,
        doAnother: doAnother
    }
})();
foo.doSomething();
foo.doAnother();
## 13.级联
启用级联可以让方法的返回值为this而不是默认值undefined .on('mousedown', function (m) {

this.starDrag(m, this.getNinth(m));
})

.later(2000, funtion() {

this

    .color('yellow')

    .setHTML('What hath God wraught?')

    .slide(400, 40, 200, 200);
})

this可以返回参数值、函数值以及属性，并且可以修改属性的尺寸和样式，添加行为

## 14.柯里化
柯里化允许我们把函数与传递给它们的参数相结合，产生出一个新的函数。

var add1 = add.curry(1);

document.writeln(add1(6));

在创建的curry方法中，如果存在Array，必须使用Array中slice方法才能产生concat方法连接两个参数数组

var slice = Array.prototype.slice,

args = slice.apply(arguments),

that=this;

return function() {

return that.apply(null, args.concat(slice.apply(arguments)));
}

## 15.记忆
函数可以将先前操作的结果记录在某个对象里，从而避免无谓的重复运算。这种优化被称为记忆。for if等语句经常被运用



