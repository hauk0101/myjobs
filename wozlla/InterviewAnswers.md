# 前端题目
###### 应答者 hauk0101
###### 日期 2016.02.26-2016.03.01  
## Javascript技术题目 
> 1.请列举一些数组元素去重方法。

作答：<br>
　　1）遍历数组法，新建数组，遍历传入数组，值不在新数组就加入该新数组中。

	//最简单的数组去重法
	function unique(array)
	{
		var n = [];
		for(var i = 0;i < array.length; i++)
		{
			if(n.indexOf(array[i] == -1))
			{
				n.push(array[i]);
			}			
		}
		return n;
	}

　　判断值是否在数组的方法“indexOf”是在ECMAScript5方法，IE8以下不支持，若用兼容低版本，则需再添加其它代码,代码如下：
	
	
	if(!Array.prototype.indexOf)
	{
		Array.prototype.indexOf = function(item)
		{
			var result = -1, a_item = null;
			if(this.length == 0)
			{
				return result;
			}
			for(var i = 0; len = this.length; i < len; i++)
			{
				a_item = this[i];
				if(a_item === item)
				{
					result = i;
					break;
				}
			}
			return result;
		}
	}

　　2）对象键值对法，新建1个js对象和1个数组，遍历传入数组时，判断值是否为js对象的键，不是的话给对象新增该键并放入新数组。（判断是否为js对象键时，会自动对传入的键执行“toString()”，不同的键可能会被误认为一样；如a[1]、a["1"]。解决此问题还是需要调用“indexOf”）

	//速度最快，占空间最多
	function unique2(array)
	{
		var n = {}, r = [], len = array.length, val ,type;
		for(var i = 0; i < array.lenght; i++)
		{
			val = array[i];
			type = typeof val;
			if(!n[val])
			{
				n[val] = [type];
				r.push(val);
			}
			else if(n[val].indexOf(type) < 0)
			{
				n[val].push(type);
				r.push(val);
			}
		}
		return r;
	}


　　3）数组下表判断法，如果当前数组的第i项在当前数组中第一次出现的位置不是i，那么表示第i项是重复的，忽略掉。否则存入结果数组。

	function unique3(array)
	{
		var n = [array[0]];
		for(var i = 1; i < array.length; i++)
		{
			if(array.indexOf(array[i] ==i))
			{
				n.push(array[i]);
			}	
		}
		return n;
	}

　　4）排序后相邻去除法，给传入数组排序，排序后相同值相邻，然后遍历时新数组只加入不与前一值重复的值。
	
	function unique(array)
	{
		array.sort();
		var re=[array[0]];
		for(var i = 1; i < array.length; i++)
		{
			if(array[i] !== re[re.length -1])
			{
				re.push(array[i]);
			}			
		}
		return re;
	}

　　5）优化遍历数组法，获取没重复的最右一值放入新数组。

	function unique5(array)
	{
		var r = [];
		for(var i = 0, l = array.length; i < l; i++)
		{
			for(var j = i + 1; j < l; j++)
			{
				if(array[i] === array[j])
				{
					j = ++i;
				}
			}
			r.push(array[i]);
		}
		return r;
	}

　　6）借助第三方类库，使用jQuery类库中unique()方法。（只适用于节点对象集合，不适用于字符串数组及数字数组）
	
	$.unique(array) //节点对象集合

> 2.Javascript的作用域和作用域链是什么？

作答：<br>
　　作用域指的是变量的适用范围。Javascript中作用域主要分为全局作用域和局部作用域（函数作用域）两种。其中全局作用域中的对象可以在代码的任何地方访问，而局部作用域中所有的变量和函数只能在其内部使用。  
　　作用域链指的是函数拥有的一个内部属性[[Scope]]中包含的能够被创建的作用域中对象的集合。它决定了哪些数据能被函数访问。
	 

> 3.Javascript的变量声明提升是什么意思？

作答：<br>
　　变量声明提升即把变量提升到函数的top的地方。其中变量提升只是提升了变量的声明，并不会把赋值也提升上来。<br>
　　还有函数提升，即把整个函数都提到前面去。由于js中函数有2种写法，一种是函数表达式，一种是函数声明方式，只有函数声明形式才能被提升。

	//函数声明方式，可提升
	function myTest1()
	{
		foo();
		function foo()
		{
			alert("我来自 foo")；
		}
	}
	myTest1();

	//函数表达式方式,不可提升
	function myTest2()
	{
		goo();
		var goo = function goo()
		{
			alert("我来自 goo");
		}
	}
	myTest2();
	
　　参考博客[http://www.cnblogs.com/betarabbit/archive/2012/01/28/2330446.html](http://www.cnblogs.com/betarabbit/archive/2012/01/28/2330446.html)

> 4.如何解决回调层次过深的问题？

作答：<br>
　　解决JS程序中回调层次过深（“回调地狱”）的方案有以下几种：<br>
　1）使用具名函数，并保持代码层级不要太深<br>

	function fun3(err,c)
	{
		// do something with a in function 3
	}
	function fun2(err,b)
	{
		// do something with b in function 2
		asyncFun3(fun3);	
	}
	function fun1(err,a)
	{
		// do something with a in function 1
		asyncFun2(fun2);
	}
	asyncFun1(fun1);


　2）使用Promise或者链式Promise<br>
　3）使用Async等辅助库，待解是需要引入额外的库，而且代码上也不够直观<br>
　4）使用Generator<br>
　5）使用CO<br>
	
　　说明：本题主要参考博客[http://www.alloyteam.com/2015/04/solve-callback-hell-with-generator/](http://www.alloyteam.com/2015/04/solve-callback-hell-with-generator/)

> 5.Ajax是指什么？jsonP是指什么？两者的原理分别是？

作答：<br>
　　Ajax全称是“Asynchronous JavaScript and XML”(异步JavaScript和XML)，它是一种在无需重新加载整个网页的情况下，能够更新部分网页的技术。它的原理是在用户和服务器之间加了一个中间层，使用户操作与服务器响应异步化。它的核心是XMLHttpRequest对象，它是Ajax实现的关键——发送异步请求、接收响应及执行回调。<br>
　　jsonP全称是“JSON with Padding”，它是一个非官方的协议，它允许在服务器端集成Script tags 返回至客户端，通过javascript callback的形式实现跨域访问。其原理是动态添加&lt;script>标签来调用服务器提供的js脚本。

## Canvas技术题目

>1.请列举十个以上常用的canvas2d的接口。

作答：<br>
　　1）createLinerGradient()：创建线性渐变（用在画布内容上）。<br>
　　2）createPattern()：在指定的方向上重复指定的元素。<br>
　　3）createRadialGradient()：创建放射状/环形的渐变（用在画布内容上）<br>
　　4）addColorStop()：规定渐变对象中的颜色和停止位置。<br>
　　5）scale()：缩放当前绘图至更大或更小。<br>
　　6）rotate()：旋转当前绘图。<br>
　　7）translate()：重新映射画布上的（0，0）位置。<br>
　　8）transform()：替换绘图的当前转换矩阵。<br>
　　9）setTransform()：将当前转换重置为单位矩阵。然后运行transform()。<br>
　　10）fillText()：在画布上绘制“被填充的”文本。<br>
　　11）strokeText()：在画布上绘制文本（无填充）。<br>
　　12）measureText()：返回包含指定文本宽度的对象。<br>
　　13）drawImage()：向画布上绘制图像、画布或视频。<br>
　　14）createImageData()：创建新的、空白的 ImageData 对象。<br>
　　15）getImageData()：	返回 ImageData 对象，该对象为画布上指定的矩形复制像素数据。<br>
　　16）putImageData()：把图像数据（从指定的 ImageData 对象）放回画布上。<br>
　　17）save()：保存当前环境的状态。<br>
　　18）restore()：返回之前保存过的路径状态和属性。<br>
　　19）createEvent()：创建自定义事件。<br>
　　20）getContext()：返回一个对象,指出访问绘图功能必要的API。<br>
　　17）toDataURL()：返回canvas图像的URL。<br>


>2.在canvas下如何优化文字的渲染速度？

作答：<br>
　　1）不是交互性文字，或动态文字绘制等需求，可直接使用位图来代替。<br>
　　2）创建一个不可见的缓冲Canvas,文字首先绘制在此Canvas上，当需要显示时，通过drawImage(canvas...)绘制到显示的Canvas上，这样可有效避免直接调用fillText带来的性能降低问题，优化文字的渲染速度。


>3.写下几种composite operation。

作答：<br>
　　canvas中的图形组合模式的属性globalCompositeOperation有12种类型：<br>
　　1）source-over(default)：默认设置，新图形会覆盖在原有内容之上。<br>
　　2）destination-over：会在原有内容之下绘制新图形。<br>
　　3）source-in：新图形会仅仅出现在与原有内容重叠的部分。其它区域都变成透明的。<br>
　　4）destination-in：原有内容中与新图形重叠的部分会被保留，其它区域都变成透明的。<br>
　　5）source-out：结果是只有新图形中与原有内容不重叠的部分会被绘制出来。<br>
　　6）destination-out：原有内容中与新图形不重叠的部分会被保留。<br>
　　7）source-atop：新图形中与原有内容重叠的部分会被绘制，并覆盖于原有内容之上。<br>
　　8）destination-atop：原有内容中与新内容重叠的部分会被保留，并会在原有内容之下绘制新图形<br>
　　9）lighter：两图形中重叠部分作加色处理。<br>
　　10）darker：两图形中重叠的部分作减色处理。<br>
　　11）xor：重叠的部分会变成透明。<br>
　　12）copy：只有新图形会被保留，其它都被清除掉。<br>	

>4.transform和setTransform接口的区别。

作答：<br>
　　画布上的每个对象都拥有一个当前的变换矩阵。其中transform()方法替换当前的变换矩阵，即允许缩放、旋转、移动并倾斜当前的环境。而setTransform()方法会先重置当前变换矩阵为单位矩阵，之后再替换为当前的需要设置的变化矩阵。

>5.请列举几个比较出名的js游戏框架。

作答：<br>
　　cocos2d-js，createjs,lufylegend,Babylon.js,Three.js, Turbulenz,Famo.us,PlayCanvas.js。<br>
　　Unity3D引擎可用js语言开发，Egret白鹭引擎是国内比较出名的Html5游戏引擎，用TypeScript语言开发。

## WebGL技术题
>1.如何兼容性地获取WebGL context?

作答：<br>
　　为了获取canvas的WebGL上下文，请求来自canvas的名为“webgl”的上下文。如果失败，尝试请求“experimental-webgl”（试验性的webgl）。如果同样失败，则显示1个警告来告诉用户，当前浏览器不只是WebGL。

	function initWebGL(canvas)
	{
		//创建全局变量
		window.gl = null;
		
		try
		{
			//尝试创建标准上下文，如果失败，回退到试验性上下文
			gl = canvas.getContext("webgl") || canvas.getContext("experimental-webgl");
		}
		catch(e){}
		
		//如果没有GL上下文，则弹出警告提示
		if(!gl)
		{
			alert("WebGL初始化失败，可能是因为您的浏览器不支持。");
		}
	}

>2.列出10个常用的WebGL接口。

作答：<br>
　　1）WebGLRenderingContext<br>
　　2）WebGLProgram<br>
　　3）WebGLActiveInfo<br>
　　4）WebGLRenderbuffer<br>
　　5）WebGLTexture<br>
　　6）WebGLBuffer<br>
　　7）WebGLShader<br>
　　8）WebGLContextEvent<br>
　　9）WebGLShaderPrecisionFormat<br>
　　10）WebGLFramebuffer<br>

>3.WebGL如何绘制图片？

作答：

>4.WebGL如何绘制文本？

作答：

>5.WebGL的pipeline是怎么样的？

作答：

>6.着色器是什么？

作答：

>7.绘制图片时Shader里必然会用到什么内置变量？

作答：

>8.drawArray和drawElements的区别？

作答：

>9.有哪些优化WebGL性能的手段？

作答：