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

@mixin flex-direction-row {
  flex-direction: row;
  -webkit-flex-direction: horizontal;
}


@mixin justify-content-center {
  justify-content: center;
  -webkit-box-pack: center;
}

//两端对齐
@mixin justify {
  justify-content: space-between;
  -webkit-box-pack: justify;
}

@mixin align-items-center {
  align-items: center;
  -webkit-box-align: center;
}

@mixin flex-number($val) {
  flex: $val;
  -webkit-box-flex: $val;
}
```

### `pointer-events` 
* `pointer-events:auto|none`，是一个css3属性，`auto`和`width:auto`一样，当值为`none`时，表现为和鼠标事件说拜拜，这里我们可以实现按钮的禁用和移动端禁止图片长按弹出框，没错，就是长按图片弹出框让你选是否保存还是取消。 

```css
//禁止图片长按弹框
img {
  pointer-events: none;
}
```
* 性能优化，移动端下拉或者上拉滚动时候，为了滚动更丝滑，可以在body上加上css `pointer-events: none;`，取消touch事件的捕获，提高性能。 
* 我们都知道获取元素可以通过选择器，但是有的时候，你并不知道选择器，比如
```html
<div class="container">
  <div class="item">
    <div class="child1"></div>
    <div class="child2"></div>
  </div>
  <div class="item">
    <div class="child1"></div>
    <div class="child2"></div>
  </div>
  <div class="item">
    <div class="child1"></div>
    <div class="child2"></div>
  </div>
</div>
```
拖着一个元素进入container元素，此时需要获取拖到了某个item上时，我们知道的唯一的信息就是此时触点的坐标，此时也许你想到可以通过(elementFromPoint)[https://developer.mozilla.org/zh-CN/docs/Web/API/Document/elementFromPoint]获取元素，但是你会发现`elementFromPoint`每次获取都是该坐标点下`z-index`最大的元素，那么还不是你拖着的元素嘛，手q群中对我的应用进行拖拽排序就遇到这样的问题。此时你可能想到设置元素的`pointer-events:none`解决。 
```javascript

```

### 高清屏下的`border-width:0.5px` 

### `-webkit-transform: translateZ(0px)` 
&emsp;css3硬件加速

### `-webkit-touch-callout` 
&emsp;禁止webview长按弹出框，比如禁止长按图片保存

### 移动端导航栏横向滚动

 



   