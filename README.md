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
## 调用
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




