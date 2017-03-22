## 那些移动端css坑

### `-webkit-overflow-scrolling`  
&emsp; 在ios上`-webkit-overflow-scrolling:touch`模拟原生的滚动效果，当你看到这个属性以为就随便用时，你会发现可能看不到满意的效果，解决办法
```css
element {
  -webkit-overflow-scrolling:touch
}
element > * {
    -webkit-transform: translateZ(0px);
}
```  
### 不是`flex`是`-webkit-box`  

### `pointer-events`


   