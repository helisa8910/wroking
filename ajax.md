
实现动态网站的技术

php--

java(jsp)

.net(微软)

Node.js--

python

.....

php

```php
page.php
  <?php
  echo'我是php后端语言，实现动态网站的技术'
  ?>
  php的标签都是运行在服务端上面的
```

php语法

```php
1.变量声明以$开头
  变量名的规则，由字符数字下划线组成并且不可以以数字开始，变量名对大小写是敏感的。
  $num=123;
	echo'哈哈';
2.字符串拼接.点
3.''单引号和双引号""是不一样的
  ''单引号对于其中的变量当作普通的字符串来处理
  ""双引号对于其中的变量会把变量解析成变得值
4.输出
 echo
  print-r
5.函数
6.转换json
  json_encode
  
```

js中处理字符串单引号和双引号的作用基本相同;

只有json格式的数据必须使用双引号

```json
var json ='{"username":"zhangsan","age":"12","sex":"male"}';
转成对象
var obj =JSON.parse(json);
conlog.dir(obj);
```

php数组

```php
<?php
  $arr = array(1,2,3,4,5);
	print_r($arr);
  ?>
1.数组的两种形式
  $arr = array(1,2,3);默认key是从0开始的整数
  $arr = array("a"=>"1","b"=>"2","c"=>"3");
二维数组
$arr = array();
$arr[0]= array(11,22,33);
$arr[1]= array(11,22,33);
$arr[2]= array(11,22,33);
print_r($arr);
自定义函数
  <?php
  function foo(Sinfo){
  return $info;
}
$ret = foo('hi');
echo $ret;
  ?>

```

js的数据类型

```javascript
基本类型：number string boolean null  undefined
引用类型：object(Array Math RegExp Date  Object Error Number String Boolen)
判断数据类型
typeof
```

http协议的常用请求方式：（增删改查）

get 用来从服务器获取数据（参数一般作为查询条件）

post用来添加数据

put 用来修改数据

delete用来删除数据

1.可以通过前端url地址传参给后台php

2.form 表单传数据

php后台文件可以根据$_post和get来获取前端的文件的值

```php
<?php
  #比如前端html有一个登录页面想要获取里面的值
$uname = $_post['username'];
$pw = $_post['password'];
//设置服务器响应的文件类型
header("Content_Type:text/plain;charset=utf-8");
if($uname=='admin'&&$pw=='123'){
  echo'登录成功'
}else{
  echo'用户名或者密码错误'
}
?>
```

案例

```查询成绩
输入你的考号就能查到成绩
getScore
<form action="./data.php"method="post">
考号：<input type="text" name="code">
	<input type="submit" value="查询">
</form>
```

1. ```php
   <?php
     //本来放在数据库里的，用假数据做
   	$code = $_POST['code'];
   获取到用户名和密码，拿去数据库匹配，如果正确，就显示相应的信息。
   ?>
   ```

json_encode()把数组或者对象转换成字符串

注：

如果从服务器上面访问后端的东西，在url地址栏上添加一些东西

locahost/data1.php?falg=2

传的是一个参数，也可以传两个参数，=用&符号链接

后台拿到falg=2的时候的处理方法

```php
<?php
  #获取参数
  $f=$_GET['flag'];
if($f==1){
  #如果f==1的时候返回123
  echo'123';
}else if($f==2){
  echo'356';
}
后台会根据你传过来的参来，给你返回相应的数据
  也就是后台接口
  ?>
```

php的请求响应的过程

```php
1.当你url地址中请求一个php页面的时候，当你点进去的时候，做了些什么？
  涉及了，前后端的交互
  服务器和php
	有一个解析器，把htmlphp,图片这些解析好了之后给服务器，服务器就传给前端
  
```

ajax

1.提交数据给后台

​	可以用form表单提交 ，填写php的地址

​	可以在url地址栏上面传值 ，写php地址传参

2.用ajax请求

```javascript
2.步准备发送用get请求
xhr.open()
它有三个参数：
	11.请求的方式（get获取数据，post提交数据）
    12，请求的地址
    13，同步或者异步标志位，默认是true表示异步，false表示同步
   14注：如果是get请求那么请求参数必须在url中传递
   var param = 'username=uname+'&password='+pw'
   xhr.open('get','02get.php？'+encodeURI(param),true);
3.执行发送动作
xhr.send(null);避免那个兼容问题
```

2.准备发送请求用post请求

```javascript
var param = 'username=uname+'&password='+pw'
   xhr.open('post','02post.php？',true);
3.执行发送动作
xhr.send(param);不需转码，参数从这里发送，但是需要设置请求头
xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded")

```

```html
处理服务端返回来的数据格式
responseText
responseXML
 

```

json数据格式

```json
json数据格式
json数据和普通的js对象的区别：
1.json数据没有变量
2.json形式的数据结尾没有分号
3.json数据中的键必须用""包住
{
  "name":"zhangsan",
  "age":12,
  "lover":["coding","swimming","shanging"],
  "friend":{
    "high":"180cm",
    "weight":"80kg",
  }
}
4.把json形式的字符串转成对象
	var str = '{"name":"zhangsan","age":"12"}';
	var obj = JSON.parse(str);
5.把对象转成字符串（调试用）
var str1 =JSON.stringify(obj);
6.早期，var d = eval()
	作用就是返字符串解析成js代码并执行
```

jsonp的本质

```javascript
<script>
  /*
  这就是jsonp的本质:动态创建script标签，然后通过它的src属性发送
  跨域请求，然后服务器端响应的数据格式为【函数调用（foo(实参)）】
  ，所以在发送请求之前必须选声明一个函数，并且函数的名字与参数中的传递的名字要一致，这里声明的函数是由服务器响应的内容（实际就是一段js代码——函数调用）来调用。
  */
  function hello(data){
  console.log(data);
}
var script = document.createElement('script');
script.src='http://tom.com/data.php    ?_cb=hello&username=zhangsan&pawwword=123';
//?号后面的-cb要和后端的文件名一样，hello要和自定义的函数名一样。
var head = document.getElementsByTagName('head')[0];
head.appendChild(script);
</script>
```

jquery封装好的jsop跨域请求

```javascript
//引入jquery.js
<body>
  <input type="button"vallue="点击" id="btn">
</body>
<script>
    $(function)(){
    $("#btn").click(function(){
      $.ajax ({
        type:'get',
        url:'http://tom.com/jsonp.php',
        dataType:'jsonp',
        jsonp:'cb',
        //jsonp属性的作用就是自定义参数名字（callback=abc这里的名字指的就是等号前面的键，后端根据这个键获取方法名，
        jquery的默认参数名称是callback）
        jsonpCallback:'abc',
        //这个属性的作用就是自定义回调函数的名字（callback+abc,这里的名字指的是等号后面的值。）
        data:{},
        success:funcion(data){
        console.log(data.username,data.password);
      },
              error:function(data){
        console.dir(data);
        console.log('error');
      }
      }) 
                    })
  }
</script>
```

 jsonp 的ajax,js

1.只支持get请求

```javascript
function ajax (obj){
  //默认值
  var defaults = {
    url:'#',
    dataType:'jsonp',
    jsonp:'callback'
    success:function(data){console.log(data);}
  }
  //采用for,in循环把参数给默认值做一个覆盖
  for(var key in obj){
    defaults[key]=obj[key]
  }
  //这里是默认的回调函数名称
  var cbName='jQuery20375850-04-_843759'
  if(defaults.jsonpCallback){
    cbName=jsonpCallback;
  }
/*
给对象添加一个属性的两个方法
var o ={};
o.info='hello';
o["info"]='hello';
[]括号填加可以传个变量
var n ='info'
o[n]="hello"


*/
  //cbName变量要作为对象的属性添加到对象里面去，window
//这里就是回调函数，调用方式：服务器响应内容来调用
//向window对象中添加一个方法，方法名称是cbName
window[cbName]=function(){
  
}
  var script = document.cgreatElement('script');
  script.src=defaults.url   +'?'+defaults.jsonp+'='+cbName;
  var head = document.getElementsByTagName('head')[0];
  head.appentdChild(cript);
}
```

promise

```javascript
1.promise:承诺，它是Es6新增的一个语法。
当你需要执行一个异步程序的时候，你可以把这个事情交给promise
promise帮你执行并且会把结果返回给你
2.promise的状态
	pedding执行中
    resolved成功状态
    	成功之后，就提供一个方法then,这方法主要是当promise执行成功之后调用。
	当异步程序执行成功并且调用resolve
    rejected失败状态
3.promise语法
	创建promise对象 let p = new Promise(function(){})
    p对象有一个参数为一个函数
    
```

/*

​	promise对象必须有一个参数，这个参数是一个回调函数

​	这个回调函数中有两个参数：

​	revsole：当回调函数执行成功之后，必须要执行revsole.

​	其实就相当于执行了promise对象的then方法。

​	reject：当异步程序执行失败之后必须执行reject(),

​		promise中提供了一个catch方法，这个方法主要是当异步程序执行失败并且调用了reject()之后执行的一个方法。

如果执行了reject,就是在执行了reject()方法。

​	这两个参数也是一个回调函数。

​	(function(revsole,reject){

​		ajax({

​	url:'..'

})

})

以上是调用promise对象的一个实参。

revsole和reject是调用function里面一个形参的名字。

*/

```javascript
let p = new Promise(function(revsole,reject){
  //写异步程序的，也就是我们的ajax
  ajax({
    url:'../api/data1.php',
    scuccess(res){
      //console.log(res) 2,3,
      //不能在这里调用，也不能在这里拿结果。
      //????如果想要data1的结果作data2的参数，data2以前方法也要在scuccess里面拿到。现在可以在than里面拿。就不用一直在scuccess里面嵌套。
      revsole(JSON.parse(res));
    }
  })
});
//console.log(p);要在这里拿到结果。把成功的结果放在than里面。如果想执行than.就跟revsole,和reject有关系。
p.then(function(res){
 // console.log(res);//拿到2和3
  ??如果想拿到data2的数据。在这里就可拿。
  let p2= new Promise(function(revsole,reject){
     ajax({
      url:'../api/data2.php',
      data:res，
      ???就是上面拿到的dat1的结果。
      scuccess(res2){
        revsole(JSON.parse(res2));
      }
    })
}) p2.then(function(data2){
   // console.log(data2); 
    //这里拿到data2的结果，//5,10
    //这里也可继续请求data.php3里面的数据。
    let p3 = promise(function(resole,reject){
       ajax({
      		url:'../api/data3.php',
         	data:data2,
         success(res3){
           resole(res3)
         }	
    	})
    })
    })p3.then(function(data3){
      console.log(data3);15
    })
```

```javascript
1.JSON.parse() 方法用于将一个 JSON 字符串转换为对象。

```

=============================

promise的高级写法

只要在then中返回promise对象，那么就可以继续then

```javascript
let p = new Promise(function(revsole,reject){
  ajax({
    url:'../api/data1.php',
    scuccess(res){
      revsole(JSON.parse(res));
    }
  })
});
p.then(function(res){
  let p2= new Promise(function(revsole,reject){
     ajax({
      url:'../api/data2.php',
      data:res，
      scuccess(res2){
        revsole(JSON.parse(res2));
      }
    })
     return p2;//就是在then中返回一个promise的对象
  }).then(function(data2){
    //console.log(data2);
    return  new Promise(function(resolve,reject){
      ajax({
      url:'../api/data3.php',
      data:res2，
      scuccess(res3){
        revsole(JSON.parse(res3));
      }
    })
    })
  }).then(function(res3){
    console.log(res3);
  })
 
  
  
  
  
  
  
  
  p2.then(function(data2){
    let p3 = promise(function(resole,reject){
       ajax({
      		url:'../api/data3.php',
         	data:data2,
         success(res3){
           resole(res3)
         }	
    	})
    })
    })p3.then(function(data3){
      console.log(data3);15
    //return p2
    })
```

封装一个promise的ajax请求

```javascript
调用
promise.html
<script src='../js/ajax.js'></script>
<script>
let p =  pAjax({
  	url:'../api/data1.php',
})p.then(function(data1){
  PAjax({
    url:'../api/data2.php',
    data:data1
  })
}).then(function(data2){
  console.log(data2);
})
</script>
```

```javascript
function PAjax(option){
  return new Promise(function(resvole,reject){
    //ajax的参数，就等于我传进来的参数
    	//ajax(option)//请求的结果没有办法调用resole
    ajax({
      url:option.url,
      data:option.data||'',
      type:option.type||'get',
      async:option.async||true,
      success(res3){
        resvole(JSON.parse(res));
      }
    })  
  })
}
```

终极解决回调地狱

```javascript
async异步
function fun(){
  console.lgo(1);
}
```

```javascript
理论：
let res1 = 10;
res1+=10;
conslo.log(res1);//20
把异步的代码当成同步的写法。
let res1=PAjax({
  url:'...'
});
let res2 =PAjax({
  url:'..//'
  data:res1
})
可以用async await
```

```javascript
async await
async 异步
async 在函数的function的前面添加，添加async之后，那么这个函数就变成一个异步的程序
想要异步的程序的结果，这个函数中必须有return,return后面的值就是这个异步程序的结果，
把异步的结果用一个p来接收的时候，返回的是值promise对象，而不是1234
当把函数变成异步程序的时候，那么这个函数的返回值是一个promise，对象，想要拿到函数return后面的值的时候，只能p.than(funtcion(res){res就是函数return的值。})
let fun = async function (){
  console.log(1);
  return:'1234'
}
let p =fun();
fun();
console.log(2);
结果21
await 等待，等待一个异步程序执行完成，await只能在async的函数中使用。
await 后面等待的是一个promise对象
await 当异步函数中遇到await,await后面还是一个promise对象的时候，那么这个await就像终止函数执行。
await 当await后面的promis对象执行结束之后，才会继续往下执行。
、、、如何表示一个promise对象执行完成？？？
·····如果执行成功：resolve 
​`````如果执行失败：reject才表示promise执行结束。

async function fun(){
  await new Promise(function(){
    console.log(1);
  })
}
fun();//调用之后1就可以直接打印出来。

async function fun(){
await new Promise(function(resolve,reject){
setTimeout(funtcion () {
	console.log('setTimeout');
	//resolve();
	//reject();
},2000)//这个时候，只有打印了setTIMeout,才会打印1，
只有当await里面的promise执行完成之后，才会执行1.要执行settimout,必须要调用resolv,或者reject. 在这个过程中，awatit,就相当于阻了同步fun的调用。去执行promisep完成之后。打印setTimeout,在打印1，之后在打印2.
})
console.log(1);
}
fun();
console.log(2);
```

````用async和await写一个数据请求
····用async和await写一个数据请求
<script src="../js/ajax.js">
<script>
	let p = PAjax({
      url:'../api/data1.php',
	})
	p.then(function(res){
      console.log(res)//2.3
	})
	 以上如果还要请求，要在p.then嵌套。
	 第二种写法：
	 fun();
	async  function fun (){
	//p.Ajax就是一个promise对象，已封好，所以这里可以用await去等待
       let p = PAjax({
      url:'../api/data1.php',
	})
	````用await去等待
	await pAjax({
	在这里不能用p.then拿到值，这么样能拿到值。
	p.then(function(res){
      console.log(res)//2.3
	})
	 }
	 
	 第三种改法
	 fun();
	 async function fun (){
	 //await可以直接把promise执行结果返回给一个变量。
    let res1=   await pAjax({
         url:'../api/data1.php',
       });
       console.log(res1)//2,3
       //这里想当于调用一个函数，拿到一个结果。如果想要执行以下代码，必须要等我执行完成之后才能执行。
       let res2 = await PAjax({
         url:'..//data2.php',
         data:res1
       });
       console.log(res2);5
       let res 3 = await PAjax({
         url:'data3',
         data:data2
       })
       console.log(res3)//15
	 }
	 //这样子完全不存在 嵌套
	 res1 就是请求出来的结果。
	 await只能写在async的函数中使用
	 await后面等待的是一个promise对象
	 promise对象执行完成
	 resolve：表示promise执行结束
	 reject:执行失败
</script>
</script>
````

数组···························

```javascript
数组：一系列的数据集合，也是一个复杂数据类型
1.定义数组
	1.1 赋值式定义数组
    var arr = [];
	1.2内置构造函数定义数组
    var arr1 = new Array();
2.创建有数据的数组
	2.1 var arr = [10,20];
	2.2 var arr1 = new Array(10);
		当只有一个参数，表示数组的长度。
        有两个参数以上的都就表示数组的数据。
3.每一个数组都是一个有序的组合。每个数组都 有一个长度length.
```

操作数组········

```javascript
var arr [];
arr[0]= 10;
arr[1] = 11;
以上可以通过数组的索引给数组添加数据。
1.定义一个数组，向数给里面添加1-50的数据。
var arr1 = new Array(50);
for (var i = 0;i<arr1.length;i++){
  arr[i]=（i+1）;
  //因为数组的索引是从0开始的。但是要最先开始的哪个数据是从1开始。
}
arr[0]='abc';
//修改数组里面的数据。把索引为0的数据修改为‘abc’

console.log(arr1);
//删除数组的里面的数据。
delete arr1[1],可以删除，返回的是empty（空的。）
？？？当索引为1的位置没有了。。不符合一系列有序的规则。

```

``` javascript
1.数组的方法
var arr = [10,20,'a','b'];
arr.push('c') //推动(push)
arr.push(40);//1.,20,a,b,c,40
1.1 push(你要添加的数据)往数组的最后追加一个数据。
	原始数组：被改变
    返回值：改变过后的数组的长度
 1.2unshift(你要添加的数据)往数组的最前面添加一个数据。
 	原始数组： 被改变
    返回值：改变过后的数组的长度。
 1.3arr.pop()没有参数，删除数组的最后一个数据。
 	原始数组：被改变
    返回值：被删除的那个数据。
 1.4shift()没有参数，删除数组的第一个数据。
 	原始数组：被改变
    返回值：被删除的那个数据。
 1.5
。
```

上。

```数组添加数据的案例

需求？
//定义一个长度为30的数组，往数组里面添加2位数的随机数。
var arr1 = new Array(30);
for(var i = 0;  i< arr.length; i++){
  arr.push(i);
}
console.log(arr[i]);
以上代码会出现死循环？？？
这种形式定会，得到一个长度为30的数组。然后从0开始，在索引为29的时候，又给添加。这个长度永远不会完。push一次，长度改变一次。然后长度就是加1了。追加一个数进去，长度变了。
解决方案例以下代码
var arr = [];
for(var i = 0; i<30;i++){
  arr.push(i)
}
console.log(arr);
//////需求要的是2个随机数
引入封装好的随机数
var arr = [];
for(var i = 0; i<30;i++){
  arr.push(getRandom(10,99))
}
console.log(arr);
```

```数组排序案例
sort方法主要是对数组进行排序
会改变原姐数组
默认按照字符的ASCII码排序
var arr = [10,20,3,4,90,2,88];
arr.sort()
以上是按ascii码排序的

？？？？？？按照数字的大小排序
sort(function(a,b)){
  return b-a
}
用法：
var arr = [10,20,3,4,90,2,88];
arr.sort(function(a,b){
  return a-b//得得升序
  return b-a//降序
})
console.log(arr);

```

```javascript
数组的方法
pop删除最后一个数据
shift删除第一个数据
？？？删除中间的数据？？？？
var arr= ['dd ','bb','cc' 'aa'];
arr.splice(2);
consloe.log(arr);
1.spice(索引，删除的个数)
如果写删除的个数，表示从index索引位置到最的数据都被删除。
还有一个用法
2.splice(index，length,value)
	用value替换删除的元素
改变原始数组
返回值：以数组的形式返回删除的数据。
3.slice(indexstart,indexend);
	3.1 slice 截取数组的数据
    	indexstart 表示开始截取的索引
        indexend:表示结束的索引（截取的数据不包含end这个索引）
        如果没有end这个参数，截取的是，从start开始的索引截取到数组最后的数据。
        如果为——1，表示结束的索引从后往前数，-1表示最后一个。-2表示到数第二个。但是截取不包含本身。
        原始数组：不改变原姐数组
        返回值：以数组的形式返回截取出来的数据。
        
```

```javasc数组的方法ript
数组的方法
var arr = [1,2,3,4,5,];
//reverse()反转数组（逆序）
console.log(arr.reverse())
1.reverse()反转数组（逆序）
改变原始数组
返回值：逆序好的数组
2.concat(6) 合并数组
参数，可以写数组，也可以写数据。就跟pop一样，往数组最后一位添加6
var res = arr.concat(arr1)
不改变原姐数组，
返回值：合并好的数组。
3.join()把数组拼接成字符串
join()里面用（给符号）
用什么样的符号拼接字符串，默认以，逗号隔开
不改变原始数组。
返回值：拼接好的字符串。


```

Es5中的循环

```javascript
var arr=[1,2,3,4,5];
arr.forEach(fcnction(item,index,arr){
            item
            })
item:代表1，2，3，4，5，数组中每一个数据。
index:下标
arr：原始数组。

```

```map
2.map()映射
	arr.map(function(item,index,arr){
      return 表达式
	})
	返回值：与原来数组长度一样的数组（根据return后面表达达式来决定新数组的内容）
var arr = [10,100,1000]
 var res = arr.map(function(item,index){
  return item*10
  //想做任何更改，就要return后面更改
})
console.log(res);
```

```javascript
3.filter()过滤
arr.fiter(function(item,index,arr){
  rteurn 条件 
})
返回值：得到一个新数组，原始数组中数据满足条件的数据。
var arr = [12,3,3,5,6,7,3,];
 var res =arr.filter(function(item){
  return item<=10
  
})
 console.log(res)//,3,3,5,6,7,3,
```

```some
4.some
var arr = [12,3,3,5,6,7,3,];
var res = arr.some(function(item,index){
	return item<=10;
	return item===6//true
})
返回值是一个boolean
some(function(item,index,arr){
  return条件
})
返回值：如果原始数组中的数有其中一个满足条件就返回true
	如果一个数据都不满足条件就返回false
```

```every
5.every:所有
every(function(item,index,arr){
  return 条件
})
返回值：如果数组中所有数扰都满足条件就返回true
如果有其中一个不满足条件就返回false
var arr = [12,3,3,5,6,7,3,];
var res = arr.every(function(item,index){
  return item>=10;//false
  所有条件都满足
})
```





