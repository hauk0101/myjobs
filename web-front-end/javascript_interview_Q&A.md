# Web前端面试题目
###### 整理者 hauk0101
## JavaScript相关部分

>1.介绍JavaScript的基本数据类型.

作答：

* 基本数据类型：Undefined、Null、Boolean、Number、String、Symbol（ES6新增，独一无二且不可变得数据类型）

>2.说说写JavaScript的基本规范？

作答：

* 不要在同一行声明多个变量
* 请使用 === / ！==来比较true / false或数值
* 使用对象字面量替代new Array这种形式
* 不要使用全局函数
* switch语句必须带有default分支
* 函数不应该有时候有返回值，有时候没有返回值
* for循环必须使用大括号
* if语句必须使用大括号
* for-in循环中的变量应该使用var关键字明确限定作用域，从而避免作用域污染

>3.JavaScript原型，原型链？有什么特点？

作答：

* 每个对象都会再起内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时，如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，于是就这样一直找下去，也就是我们平时所说的原型链的概念。
* 关系：instance.constructor.prototype = instance.__proto__
* 特点：JavaScript对象通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，与之相关的对象也会继承这一改变。
* 当我们需要一个属性时，Javascript引擎就会先看当前对象中是否有这个属性，如果没有的话，就会查找他的Prototype对象是否有这个属性，如此递推下去，一直检索到Object內建对象。

		function Func(){};
		Func.prototype.name = "Sean";
		Func.prototype.getInfo = function(){
			return this.name;
		}
		var person = new Func();	//现在可以参考var person = Object.create(oldObject);
		console.log(person.getInfo());	//它拥有了Func的属性和方法
		//输出“Sean”
		console.log(Func.prototype);
		//输出“Func{name="Sean",getInfo=function()}”

>4.JavaScript有几种类型的值？（堆：原始数据类型，栈：引用数据类型），你能画一下他们的内存图吗？

作答：

>5.JavaScript如何实现继承？

作答：

* 构造继承
* 原型继承
* 实例继承
* 拷贝继承
* 原型prototype机制或apply和call方法去实现较简单，建议使用构造函数与原型混合方式
		
		function Parent(){
			this.name = "wang";
		}
		function Child(){
			this.age = 25;
		}
		Child.prototype = new Parent();//继承了Parent,通过原型
		var demo = new Child();
		console.log(demo.age);
		console.log(demo.name);//得到被继承的属性

>6.JavaScript创建对象的几种方式？

作答：

>7.JavaScript作用链域？

作答：

* 全局函数无法查看局部函数的内部细节，但局部函数可以查看其上层的函数细节，直至全局细节。
* 当需要从局部函数查找某一属性或方法时，如果当前作用域没有找到，就会上溯到上层作用域查找，直至全局函数，这种组织形式就是作用域链。

>8.谈谈this对象的理解。

作答：

* this总是指向函数的直接调用者（而非间接调用者）
* 如果有new关键字，this指向new出来的那个对象
* 在事件中，this指向触发这个事件的对象，特殊的是，IE中attachEvent中的this总是指向全局对象Window
>9.eval是做什么的？

作答：

* 它的功能是把对应的字符串解析成JS代码并运行；
* 应该避免使用eval,不安全，非常消耗性能（2次，一次解析成js语句，一次执行）
* 由JSON字符串转化为JSON对象的时候可以用eval,var obj = eval('('+str+')');

>10.什么是window对象？什么事document对象？

作答：

* window对象是指浏览器打开的窗口
* document对象时Document对象（HTML文档对象）的一个只读引用，window对象的一个属性

>11.null，undefined的区别？

作答：

>12.写一个通用的事件侦听器函数.

作答：

>13.["1","2","3"].map(parseInt)答案是多少？

作答：

>14.关于事件，IE与火狐的事件机制有什么区别？如何阻止冒泡？

作答：

>15.什么是闭包（closure），为什么要用它？

作答：

>16.JavaScript代码中的“use strict”是什么意思？使用它的区别是什么？

作答：

>17.如何判断一个对象是否属于某个类？

作答：

>18.new操作符具体干了什么呢？

作答：

>19.用原生JavaScript的实现过什么功能呢？

作答：

>20.JavaScript中，有一个函数，执行时对象查找时，永远不会去查找原型，这个函数是？

作答：

>21.对JSON的了解？

作答：

>22.[].forEach.call($$("*"),functin(a){a.style.outline="1px solid #" + (~~(Math.random()*(1<<24))).toString(16)})能解释一下这段代码的意思吗？

作答：

>23.js延迟加载的方式有哪些？

作答：

>24.Ajax是什么？如何创建一个Ajax?

作答：

>25.同步和异步的区别？

作答：

>26.如何解决跨域问题？

作答：

>27.页面编码和被请求的资源编码如果不一致如何处理？

作答：

>28.模块化开发怎么做？

作答：

>29.AMD(Modules/Asynchronous-Definition)、CMD（Common Module Definition）规范区别？

作答：

>30.requireJS的核心原理是什么？（如何动态加载的？如何避免多次加载的？如何缓存的？）

作答：

>31.让你自己设计实现一个requireJS,你会怎么做？

作答：

>32.谈一谈你对ECMAScript6的了解？

作答：

>33.ECMAScript6怎么写class么，为什么会出现class这种东西？

作答：

>34.异步加载的方式有哪些？

作答：

>35.document.write和innerHTML的区别？

作答：

>36.DOM操作——怎样添加、移除、移动、复制、创建和查找节点？

作答：

>37. .call()和.apply()的含义和区别？

作答：

>38.数组和对象有哪些原生方法，列举一下？

作答：

>39.JS怎么实现一个类。怎么实例化这个类。

作答：

>40.JavaScript中的作用域和变量声明提升？

作答：

>41.如何编写高性能的JavaScript？

作答：

>42.哪些操作会造成内存泄漏？

作答：

>43.jQuery的源码看过吗？能不能简单概括一下它的实现原理？

作答：

>44.jQuery.fn的init方法返回的this指的是什么对象？为什么要返回this？

作答：

>45.jQuery中如何将数组转化为json字符串，然后再转化回来？

作答：

>46.jQuery的属性拷贝（extend）的实现原理是什么？如何实现深拷贝？

作答：

>47.jQuery的队列是如何实现的？队列可以用在哪些地方？

作答：

>48.谈一下jQuery中的bind()，live()，delegate()，on()的区别？

作答：

>49.jQuery一个对象可以同时绑定多个事件，这是如何实现的？

作答：

>50.是否知道自定义事件。jQuery里的fire函数是什么意思，什么时候用？

作答：

>51.jQuery是通过那个方法和Sizzle选择器结合的？（jQuery.fn.find()进入Sizzle）

作答：

>52.针对jQuery性能的优化方法？

作答：

>53.jQuery和jQuery UI有啥区别？

作答：

>54.jQuery和Zepto的区别？各自的使用场景？

作答：

>55.Zepto的点透问题如何解决？

作答：

>56.jQueryUI如何自定义组件？

作答：

>57.需求：实现一个页面操作不会整页刷新的网站，并且能在浏览器前进、后退时正确响应，给出你的技术实现方案？

作答：

>58.如何判断当前脚本运行在浏览器还是node环境中？

作答：

>59.移动端最小触控区域是多大？

作答：

>60.jQuery的slideUp动画，如果目标元素是被外部事件驱动，当鼠标快速地连续触发外部元素事件，动画会滞后的反复执行，该如何处理呢？

作答：

>61.把Script标签放在页面的最底部的body封闭之前和封闭滞后有什么区别？浏览器会如何解析它们？

作答：

>62.移动端的点击事件的有延迟，时间是多久，为什么会有？怎么解决这个延时？(click有300ms延迟，为了实现safari的双击事件的设计，浏览器要知道你是不是要双击操作)

作答：

>63.知道各种JS框架（Angular,Backbone,Ember,React,Meteor,Knockout...）么？能讲出它们各自的有点和缺点么？

作答：

>64.Underscore对哪些JS原生对象进行了扩展以及提供了哪些好用的函数方法？

作答：

>65.解释JavaScript中的作用域与变量声明提升？

作答：

>66.Node.js的适用场景？

作答：

>67.知道route,middleware,cluster,nodemon,pm2,server-side rendering么（node.js相关）？

作答：

>68.解释一下Backbone的MVC实现方式？

作答：

>69.什么是“前端路由”？什么时候适合使用“前端路由”？“前端路由”有哪些优点和缺点？

作答：

>70.知道什么是webkit么？知道怎么用浏览器的各种工具来调试和debug代码么？

作答：

>71.如何测试前端代码？知道BDD,TDD,Unit Test么？知道怎么测试你的前端工程么？（mocha,sinon,jasmin,qUnit...）？

作答：

>72.前端templating(Mustache，underscore,handlebars)是干嘛的，怎么用？

作答：

>73.简述一下Handlebars的基本用法？

作答：

>74.简述一下Handlebars的对模板的基本处理流程，如何编译的？如何缓存的？

作答：

>75.用js实现千位分隔符？（来源：前端农民工，提示：正则+replace）

作答：

>76.检测浏览器版本有哪些方式？

作答：

>77.我们给一个dom同时绑定两个点击事件，一个用捕获，一个用冒泡，你来说下会执行几次事件，然后会先执行冒泡还是捕获。

作答：