---
layout: post
title: Google 三维 JavaScript API 发布
date: 2009/4/22/ 4:1:41
updated: 2009/4/22/ 4:1:41
status: publish
published: true
type: post
---

O3D 是一个开源的Web API，其可以创建相当牛X的基于浏览器的可交互式的3D应用。这个API在很有可能会形成以后的Web上的3D图形的标准。下面是这个API的主站点： <http://code.google.com/apis/o3d/> 。O3D目前支持Windows, Mac和Linux三种平台。


下面是一些简单地使用O3D的API的如何创建一个立方体，更详细的内容请访问O3D的网站。


1）首选我们先创建一个比较原始的立方体。使用createCube()方法。


[javascript]


function createCube(material) {  

 var cubeShape = g\_pack.createObject(‘Shape’);  

 var cubePrimitive = g\_pack.createObject(‘Primitive’);  

 var streamBank = g\_pack.createObject(‘StreamBank’);


 cubePrimitive.material = material;  

 cubePrimitive.owner(cubeShape);  

 cubePrimitive.streamBank = streamBank;  

 .  

 .  

 .  

[/javascript]


  

 2）然后，我们需要指定一些顶点信息。  

其中，我们利用三角形来构造3D图形。一个立方体有12个三角面，两个构成一个面，然后有8个顶点。  

[javascript]  

 cubePrimitive.primitiveType = g\_o3d.Primitive.TRIANGLELIST;  

 cubePrimitive.numberPrimitives = 12; // 12 triangles  

 cubePrimitive.numberVertices = 8; // 8 vertices in total  

 cubePrimitive.createDrawElement(g\_pack, null); // Create the draw element for this primitive.  

[/javascript]


3）指定一下8个顶点的坐标。  

[javascript]  

var positionArray = [  

 -0.5, -0.5, 0.5, // vertex 0  

 0.5, -0.5, 0.5, // vertex 1  

 -0.5, 0.5, 0.5, // vertex 2  

 0.5, 0.5, 0.5, // vertex 3  

 -0.5, 0.5, -0.5, // vertex 4  

 0.5, 0.5, -0.5, // vertex 5  

 -0.5, -0.5, -0.5, // vertex 6  

 0.5, -0.5, -0.5 // vertex 7  

 ];  

[/javascript]


4）把顶点坐标数组加入Buffer中。  

[javascript]  

// Create buffers containing the vertex data.  

var positionsBuffer = g\_pack.createObject(‘VertexBuffer’);  

var positionsField = positionsBuffer.createField(‘FloatField’, 3);  

positionsBuffer.set(positionArray);  

[/javascript]


5）把Buffer放到Stream Bank中。


[javascript]  

// Associate the positions Buffer with the StreamBank.  

streamBank.setVertexStream(  

 g\_o3d.Stream.POSITION, // semantic: This stream stores vertex positions  

 0, // semantic index: First (and only) position stream  

 positionsField, // field: the field this stream uses.  

 0); // start\_index: How many elements to skip in the field.  

[/javascript] 


6）连接点成为三角面，并把三角面两两一组组成立方面。  

[javascript]  

var indicesArray = [  

 0, 1, 2, // face 1  

 2, 1, 3,  

 2, 3, 4, // face 2  

 4, 3, 5,  

 4, 5, 6, // face 3  

 6, 5, 7,  

 6, 7, 0, // face 4  

 0, 7, 1,  

 1, 7, 3, // face 5  

 3, 7, 5,  

 6, 0, 4, // face 6  

 4, 0, 2  

 ];  

[/javascript]


完整的源码请参看这里：（打开网页后查看源码）  

<http://o3d.googlecode.com/svn/trunk/samples/hellocube.html>


最后，让我们看一看下面YouTube上的视频，你就知道这个东西有多强了。[YouTube链接](http://www.youtube.com/watch?v=uofWfXOzX-g)。




**（转载本站文章请注明作者和出处 [酷 壳 – CoolShell](https://coolshell.cn/) ，请勿用于任何商业用途）**



### 相关文章

* [![我看ChatGPT: 为啥谷歌掉了千亿美金](../wp-content/uploads/2023/02/chatgpt-150x150.jpg)](https://coolshell.cn/articles/22398.html)[我看ChatGPT: 为啥谷歌掉了千亿美金](https://coolshell.cn/articles/22398.html)
* [![程序员练级攻略（2018)  与我的专栏](../wp-content/uploads/2018/05/300x262-150x150.jpg)](https://coolshell.cn/articles/18360.html)[程序员练级攻略（2018) 与我的专栏](https://coolshell.cn/articles/18360.html)
* [![Chrome开发者工具的小技巧](../wp-content/uploads/2017/01/pretty-code-150x150.gif)](https://coolshell.cn/articles/17634.html)[Chrome开发者工具的小技巧](https://coolshell.cn/articles/17634.html)
* [![如何读懂并写出装逼的函数式代码](../wp-content/uploads/2016/10/drawing-recursive-150x150.jpg)](https://coolshell.cn/articles/17524.html)[如何读懂并写出装逼的函数式代码](https://coolshell.cn/articles/17524.html)
* [![Google Inbox如何跨平台重用代码？](../wp-content/uploads/2014/11/inbox2-640x264-150x150.jpg)](https://coolshell.cn/articles/12136.html)[Google Inbox如何跨平台重用代码？](https://coolshell.cn/articles/12136.html)
* [![函数式编程](../wp-content/uploads/2013/12/yoda-lambda-150x150.png)](https://coolshell.cn/articles/10822.html)[函数式编程](https://coolshell.cn/articles/10822.html)
The post [Google 三维 JavaScript API 发布](https://coolshell.cn/articles/599.html) first appeared on [酷 壳 - CoolShell](https://coolshell.cn).