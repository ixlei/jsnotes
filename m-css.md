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
&emsp;基于盒模型，依赖`display`，`position`，`float`属性实现布局时有很多布局很难实现，比如垂直居中。依赖flex的弹性布局将会是一个很好的解决方案，`flex`在ios上支持已经很好了，但是像uc浏览器这种兼容性是很大的问题，所以请用`-webkit-box`
```css
@mixin flex {
  display: flex;
  display: -webkit-box;
}
```

### `pointer-events`

### 高清屏下的`border-width:0.5px` 



   