---
title: createjs小游戏笔记
tags:
  - 前端
  - createjs
categories: 前端
abbrlink: 6052
date: 2021-07-09 00:37:05
---
1. 创建舞台
```javascript
let stage = new createjs.Stage();//()中为画布的id,与画布进行绑定
```
2. 创建容器
```javascript
let gameView = new createjs.Container();
stage.addChild(gameView);//可将容器放在舞台中，创建的元素放在容器中
stage > container > 单个元素//三代之间的关系，可通过addChild()方法进行追加元素
```
3. 创建图形
```javascript
let shape = new createjs.Shape();//创建一个图形
shape.graphics.beginFill(color)drawRect(x,y,w,h);//画一个矩形
shape.graphics.beginFill(color)drawRoundRect(x,y,w,h,radius);//画圆角矩形
shape.graphics.beginFill(color)drawCircle(x,y,r);//画圆
```
4. 创建图片
```javascript
let img = new createjs.Bitmap();//括号中为图片路径
```
5. 创建文字
```javascript
let text = new createjs.Text(text,font,color);//创建文字
//属性
text.lineWidth  //设置行宽
text.lineHeight //设置行高
text.textAlign  //设置对齐方式
注：
当设置左对齐的时候，text.x的值为文字的起始点横坐标；
当设置右对齐的时候，text.x的值为文字的结束点横坐标；
当设置居中对齐的时候，text.x的值为文字的中间点横坐标；
当设置lineWidth会出现中文不换行问题见19；
```
6. 常见属性和方法
```javascript
demo.x //设置起始位置横坐标
demo.y //设置起始位置纵坐标
demo.alpha //设置透明度
demo.x //设置起始位置横坐标
demo.y //设置起始位置纵坐标
demo.scaleX //水平变换
demo.scaleY //垂直变换
demo.scale  //整体变换
demo.alpha  //设置透明度
demo.mask   //设置蒙版
demo.name   //设置名称
demo.visible //设置元素是否显示 
demo.removeAllChildren(); //移除所有子元素
parent.addChild(child); //添加子元素
parent.setChildIndex(child,parent.getNumChildren()-num);//设置层级
注：
1. 当alpha为0时不能触发事件；
2. mask显示的内容为和蒙版重合的部分，为蒙版不追加入img的父元素中；
```
7. 雪碧图
```javascript
let data = {
    images: [url],//图片路径
    frames: {width:w,height:h,count:count},//w,h是一张精灵图的实际宽高，count的图片数量
    animations: {
        run: {
            frames:[0,3],//显示哪几张图片，0，3为0～3四张
            speed:0.5 //图片运动速度
        },
    }
};
let spriteSheet = new createjs.SpriteSheet(data);
let animation = new createjs.Sprite(spriteSheet,"run");
nimation.set({x:x,y:y,scaleX:scaleX,scaleY:scaleY});
```
8. 创建动画
```javascript
createjs.Tween.get(元素).to({属性:值},时间)；//异步执行
createjs.Tween.get(元素).to({属性:值},时间).call(function(){})；//function()和动画同步执行，会在动画结束后执行
```
9. 资源预加载
```javascript
$.when(filePreload()).then(function(){});
//预加载完成后在执行then后面的函数
function filePreload(){
    //deferred对象的含义就是"延迟"到未来某个点再执行。
    let deferred = new $.Deferred();
    //preload可以方便我们预先加载相关资源
    let queue = new createjs.LoadQueue(false);
    //如果载入声音，必须先注册createjs.Sound
    queue.installPlugin(createjs.Sound);
    //将需要预加载的资源放在manifest数组中
    //url：资源的路径
    //id:给资源重新定义的名字，调用改资源时使用
    let manifest = [
        {id:id,src:url"}
    ];
    //预加载过程中执行的函数
    //当调用某一资源时使用bitmapList[id].clone(),且bitmapList需为全局变量
    queue.on("fileload", function (event) {
        if (event.item.type == "image") {
            bitmapList[event.item.id] = new createjs.Bitmap(event.result);
            }
        }
    }, this);
    //预加载完成后执行的函数
    queue.on("complete", function (event) {
        deferred.resolve();
    }, this);
    queue.loadManifest(manifest);
    return deferred.promise();
}
```
10. 设置旋转(竖屏转成横屏) 
```javascript
stage.rotation = 90;
stage.x = screenWidth;
stage.y = 0;
let temp = screenWidth;
screenWidth = screenHeight;
screenHeight = temp;
注：等号右侧为竖屏宽高，左侧为横屏宽高
```
11. 当使用高清图片时若图片还是不清晰，可适当扩大画布的倍数；
12. 当使用onload方法且需要传参时，避免异步的影响
```javascript
//如加载图片时，图片没有加载好就获取图片属性会报错
//若在for循环中，可能计数i会产生影响
let img = new Image();
img.src = url;
img.index = 1;
img.onload = function(){
    console.log(img.index);
}
//可推广
let obj = {};
obj.x = 1;
obg.onload = function(){
    console.log(obj.x);
}
```
13. 动态修改shape图形的参数
```javascript
shape.graphics.command.属性 = 值；
```
14. 实现container的滚动
```javascript
//主函数
if(createjs.Touch.isSupported() == true){
        createjs.Touch.enable(stage)
    }
//设置滚动条件
let localPos,y;
gameView.addEventListener('mousedown',function(evt){
    //滑动开始时的位置
    let stageX = evt.stageX;
    let stageY = evt.stageY;
    //将gameView对象从舞台（全局）坐标转换为显示对象的（本地）坐标
    localPos = stage.globalToLocal(stageX,stageY);
    //获取gameview对象的坐标
    y = gameView.y;
})
gameView.addEventListener('pressmove',function(evt){
    //gameview.y = 滑动结束时滑动点处的y-滑动开始时滑动点处的y+滑动开始时gameview的y
    let move_y = evt.stageY - localPos.y + y;
    //通过滑动区域y坐标的大小限制滑动区域
    if(move_y >= -(滑动区域.y-显示区域.y) && move_y <= 0){
        gameView.y = move_y;
    }
})
```
15. 全局只需要在入口函数设置tick刷新舞台即可；
16. 适配不同的手机屏幕可通过长宽比例进行适配； 
17. js合并两个数组
```javascript
arr1 = arr1.concat(arr2);
```
18. 获取屏幕的宽高
```javascript
let screenWidth = window.innerWidth;
let screenHeight = window.innerHeight;
```
19. EaselJS的Text中文不会自动换行的问题
修改easeljs的p._drawText方法为
[点击](https://pasteme.cn/135634)
20. 解决createjs的点击图片跨域问题

    ```javascript
    //在图片上面盖上一个形状，使图片不触发单击时间
    var hitArea = new createjs.Shape();
    hitArea.graphics.beginFill("#000").drawRect(0,0,92,92);//这里是图片大小
    bitmap.hitArea = hitArea;
    ```