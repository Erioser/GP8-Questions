###  GP8面试积累资料

#### 课堂模拟面试

1. 离职原因？

   实话实说就ok，公司平台转型了。没有新项目了。经营不善。注意，千万不要骂上一家公司！交接清楚了。

2. 回流和重绘？

   reflow：dom树结构改变，可能是其中的某个块级元素display：none的时候；浏览器需要重新渲染dom文档中大部分结构。

   repaint ：dom的表现形式变化，不影响整个dom树结构，例如：div的背景颜色/字体颜色变化；浏览器只需要重新渲染改变的一小部分就可以。

   哪怕重绘也尽量别回流。

3. 对前端工程化有什么理解?

   在前端开发的过程中，使用gulp/grunt/webpack等基于node环境的前端自动化工具来搭建前端自动化环境，利用npm/bower/yarn这样的包管理器去管理环境中使用的工具包来实现想要的功能，利用这样的环境来进行高效快速的开发的形式叫前端工程化。

4. JS的兼容问题及解决方案。

   。。。。。。。

5. 项目优化方案或方向。

   SEO优化/前端性能优化

   前端性能优化（《雅虎十四条》）：

   * http请求优化
   * 压缩合并文件
   * 。。。

6. promise和setTimeout的执行顺序

   ```
          setTimeout(() => {
               console.log(1)
           }, 0);
   
           new Promise(function (resolve, rejected) {
               console.log(2);
               setTimeout(function() {
                   resolve();
               },10)
               // for (let i = 0; i <10000; i++) {
               //     if ( i === 9999 ) {
               //         resolve();
               //         break;
               //     }
               // }
               console.log(3);
           }).then(() => {
               console.log(4);
           })
   
           console.log(5);
   
           // js是单线程的，所以既然在js运行过程中，有某些动作因为是异步的，可能会顺序颠倒，但是也是挨个执行的。
   
           // 我们可以把这个执行的顺序链分为两段：同步队列，异步队列，同步队列代码运行完成后再去执行异步队列的代码
   
           // 首先会先执行setTimeout，里面的回调函数因为是异步代码，所以 console.log(1) 会放入到异步队列中
   
           // 接下来会执行promise中的回调函数，所以先执行console.log(2);但是，reslove执行后，理论上应该执行then中的回调函数了，但是不是这样的，就算resolve执行了，依然会先把当前的回调函数执行完毕
   
           // 所以执行了console.log(3)；然后此时，同步队列中还有console.log(5);没有再执行，所以继续执行console.log(5);
   
           // 到现在为止，同步队列执行完成了。开始执行异步队列，而promise中的then回调函数中的异步函数往往会根据resolve执行的顺序来执行
   
           // 如果影响resolve执行的是同步的，resolve所代表的then中的回调函数就会放在异步队列的前边，而其他的setTimeout的回调放在后边
   
   ```

7. call和apply

   用来在调用函数的时候去改变函数中的this指向并且传递参数

   call传递参数的时候是散列传递，apply是以数组的形式传递的。

8. undefined和null的区别

   这两种都属于数据类型中的数据类型。

   undefined代表未定义，null代表值为空

   在定义变量后没有赋值的时候，变量的值暂时为undefined

9.  link导入样式和@import导入样式的区别

   引入方式：

   link是html标签，通过在html文件中引入，@import在css文件中引入

   兼容性：

   link没有兼容性问题，@import 需要在IE5以上才生效

   css优先级：

   同等权重的样式的优先级：行内样式、内联样式、外联样式、导入样式 
    外联样式和导入样式都有一个`div{background:XX}`,最终的div样式是外联样式中所定义div样式

   加载顺序：

   link是在加载html文档的时候加载，而如果@import是在外联的css文件中使用，那么@import引入顺序就是在最后面了。 

10. javascript种常见报错的类型

    unexpected token  语法错误；

    .. is not define  变量不存在

    can not set property abc of undefined/null  变量/指针丢失 ... 

    ....

11. childNode和chidlren

    childNodes：获取节点，不同浏览器表现不同；

    　　IE：只获取元素节点；

    　　非IE：获取元素节点与文本节点；

    解决方案：if(childNode.nodeName=="#text") continue 或者 if(childNode.nodeType != '3') continue 

    children：获取元素节点，浏览器表现相同。

    　　因此建议使用children。

12.  垃圾回收机制策略

    现在各大浏览器通常用采用的垃圾回收有两种方法：标记清除、引用计数。

    [参考地址](https://www.cnblogs.com/zhwl/p/4664604.html)

13. 前端存储方案

    存储的场景：

    * 缓存
    * 通信 （标签页之间/前后端）
    * 数据共享

    全局变量/cookie/webstorage
