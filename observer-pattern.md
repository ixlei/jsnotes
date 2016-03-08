##观察者模式

>当一个或者多个观察者对某个目标感兴趣，通过将自己依附在目标上以便注册感兴趣的内容，当目标的状态发生改变，目标通知观察者状态改变。这就是观察者模式。在前端中，观察者模式很常见。
`ele.onclick = callback`,事件的捕获就是一个例子。

>观察者模式中有两个对象，目标`subject`和`observer`,`subject`负责对观察者的管理，`observer`负责对目标状态发生改变作出响应。

```javascript

'use strict';
class Pubsub {
    constructor() {
      this.topicList = new Map();
      this.sticky = new Map();
    }

   on(topic, listener) {
 	let topicList = this.topicList,
 	    sticky = this.sticky;
    if(!topicList.has(topic)) {
      topicList.set(topic, []);
    }
    let listenerList = topicList.get(topic);
    listenerList.push(listener);
    if(sticky.has(topic)) {
      let state = sticky.get(topic);
      listener(state);
    }
 }

 trigger(topic, state) {
   let topicList = this.topicList,
       sticky = this.sticky;
    sticky.set(topic, state);
    let listenerList = topicList.has(topic) ? topicList.get(topic) : [];
    for(let listener of listenerList) {
      listener(state);
    }
 }
 
 remove(topic, lisener) {
   let topicList = this.topicList,
       listenerList = topicList.has(topic) ? topicList.get(topic) : [],
       index = listenerList.indexOf(listener);
    if(index !== -1) {
      listenerList.splice(index, 1);
    }
 }
}
```