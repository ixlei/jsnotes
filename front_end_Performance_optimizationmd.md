##前端性能优化

##网络请求优化

* 设置缓存。缓存的种类很多，浏览器缓存是其中之一，在浏览器缓存中又分为强缓存和协商缓存。

* 压缩资源。减少资源的大小加快响应，压缩js,css文件，删除不必要的css文件。

* 使用多个域名来加快响应，由于浏览器并发限制是基于domain的，所以使用多个域名可以加快响应，但是会怎增大域名解析时间，所以一般会用2-4个域名。

* cookie隔离，静态资源的请求没有必要验证cookie,所以把静态资源放在主域下，每次请求都会携带cookie,加大请求响应大小，而且服务器会对cookie解析。所以可以把静态资源放置在另外一个服务器上。

* 通过设置延迟(deffer)和异步(async)脚本加快资源下载解析；可以动态插入脚本，按需加载；也可以延迟加载。

* 合并HTTP请求，合并css，js文件，使用雪碧图或者制作icon font来减少图片请求。

* 如果在url小于2k时使用GET请求,GET请求快于POST请求。

* 避免重定向。


##js优化

### DOM结点操作优化，DOM的操作会会发生回流和重绘，所以合并DOM操作是提升性能的有效手段。

*  使用增加class和删除class来减小因为样式设置引起的回流和重绘。

*  DOM插入时使用创建一个dom容器，使用`createDocumentFragment`。后整体插入。

*  操作某个元素时可以先使元素离线，即使用`cloneNode`来克隆一份，再使用`replaceChild`替换。

* 对于`offsetWidth`, `offsetHeight`, `scrollHeight`, scrollWidth`, `scrollTop`, `scrollLeft`的获取，可以使用变量来保存，不必要每次都调用api获取，会重新计算文档。

* 避免使用`getElementsByTagName('*')`来取得元素。

###事件优化

* 利用时间冒泡机制，事件代理，减少事件绑定。
* 对`scroll`和`resize`事件，应该去除抖动。
* 记得使用`removeEventListener`, `detachEvent`, `ele.onclick = null`。

## css优化

* 使用className来更换样式。
* 对于动画，设置`position`为`absolute`或者`fixed`更好。
* 避免使用table布局，每个元素的改变都会引起整个元素的调整。
* 避免使用样式表达式。
* 把css样式放置在头部。


##参考链接

* [discussion-on-web-caching](http://www.alloyteam.com/2016/03/discussion-on-web-caching/)

* [Web缓存的工作原理](http://www.alloyteam.com/2012/03/web-cache-2-browser-cache/#prettyPhoto)

* [浏览器缓存](http://www.cnblogs.com/lyzg/p/5125934.html)

* [浏览器允许的并发请求资源数](https://www.zhihu.com/question/20474326)

* [翻译：web制作、开发人员需知的Web缓存知识](http://www.zhangxinxu.com/wordpress/2013/05/caching-tutorial-for-web-authors-and-webmasters/)

* [no-cache&no-store](http://stackoverflow.com/questions/866822/why-both-no-cache-and-no-store-should-be-used-in-http-response)

* [探讨css中repaint和reflow](http://www.cnblogs.com/shenqi0920/p/3545820.html)

* [页面重绘和回流以及优化](http://blogread.cn/it/article/6900?f=sa)

* [查询哪些属性会引起repaint或reflow](https://csstriggers.com/)

* [如何稀释onscroll事件](http://segmentfault.com/q/1010000000707337)

* [图片延迟加载](http://www.cnblogs.com/tugenhua0707/p/3515292.html)

* [jquery委托设计](http://www.cnblogs.com/aaronjs/p/3447483.html)