---
title: 自用AE表达式
date: 2024-09-27 20:30:00 +800
categories: [AE, AE资源]
tags: [AE, 表达式]     # TAG names should always be lowercase
description: 个人之前写的After Effects表达式
pin: false
---

## 表达式学习相关链接：
[Con幺幺的AE学习笔记](https://space.bilibili.com/1762926/channel/collectiondetail?sid=185180)<br />
[月离AE表达式文档](https://docs.yuelili.com/#/book/Ae/expression)<br />
[鹤梦表达式增强库](https://github.com/dreamstring/Leaf)
## 标记字幕表达式

### 基于标记生成字幕
支持混合使用普通标记和有持续时间的标记，将表达式添加到带有标记的文本层使用。
```javascript
m = thisLayer.marker.nearestKey(time);
//寻找最近的标记
function ifZero(){
	if(m.index-1==0){
		return ""
	}else{
		return ifDuration(m.index-1)
	}
}
//判断是否为零，如果零输出空值
function ifDuration(a){
	var kayA=thisLayer.marker.key(a);
	if(kayA.duration==0){
		return thisLayer.marker.key(a).comment
	}else{
		if(time <= kayA.time+kayA.duration){
			return thisLayer.marker.key(a).comment
		}else{
			return ""
		}
	}
}
//判断标记是否有持续时间，如果有，判断当前时间是否在持续时间内
if(m.time <= time){
	ifDuration(m.index)
}else{
	ifZero()
}
```

### 基于图层标记时间映射动画
同上，支持混合使用普通标记和有持续时间的标记，示例表达式可用于图层透明度属性。<br />
将表达式添加到带有标记的文本层，或者添加到其他图层将layer1修改为文本层使用。<br />
建议学习：[AE文本动画文档](https://docs.yuelili.com/#/post/Ae/basic/zh/text-animation/Expression-Selector.md)<br />
配合使用可以做出许多有趣的效果。
```javascript
//V1.02 by Con11
//数组需要按照例如[100,100]的格式输入数值

inValue=0;//进入数值
stayValue=100;//一般数值
outValue=0;//退出数值
aniTime=0.5;//动画时间
aniDely=0;//动画延迟
linearTrue=false;//是否线性,true为线性，false为缓动
layer1=thisLayer;//图层

m = layer1.marker.nearestKey(time);
//寻找最近的标记
function ifZero(){
	if(m.index-1==0){
		return ""
	}else{
		return ifDuration(m.index-1)
	}
}
//判断是否为零，如果零输出空值
function ifDuration(a){
	var kayA=layer1.marker.key(a);
	if(kayA.duration==0){
		return layer1.marker.key(a).index
	}else{
		if(time <= kayA.time+kayA.duration){
			return layer1.marker.key(a).index
		}else{
			return ""
		}
	}
}
//判断标记是否有持续时间，如果有，判断当前时间是否在持续时间内
if(m.time <= time){
	nowMark=ifDuration(m.index);
}else{
	nowMark=ifZero();
}

function linearIn(a){
	return linear(time,a,a+aniTime,inValue,stayValue)
}
function linearOut(a,b,c){
	if(layer1.marker.key(nowMark).duration==0){
		return linear(time,c-aniTime,c,stayValue,outValue)
	}else{
		return linear(time,a+b-aniTime,a+b,stayValue,outValue)
	}

}
//线性出入
function toEaseIn(a){
	return ease(time-aniDely,a,a+aniTime,inValue,stayValue)
}
function toEaseOut(a,b,c){
	if(layer1.marker.key(nowMark).duration==0){
		return ease(time-aniDely,c-aniTime,c,stayValue,outValue)
	}else{
		return ease(time-aniDely,a+b-aniTime,a+b,stayValue,outValue)
	}

}
//缓动出入
if(nowMark==""){
	inValue
	//如果索引是空返回进入值
}else{
	markTime=layer1.marker.key(nowMark).time;
	if(layer1.marker.nearestKey(outPoint).index==nowMark){//判断是否为最后一个标记
		markTime1=outPoint
	}else{
		markTime1=layer1.marker.key(nowMark+1).time;
	}
	
	markDuration=layer1.marker.key(nowMark).duration;
	if(linearTrue==true){//判断是否为线性
		if(time <= markTime+aniTime){
			linearIn(markTime)
		}else{
			linearOut(markTime,markDuration,markTime1)
		}
	}else{
		if(time <= markTime+aniTime){
			toEaseIn(markTime)
		}else{
			toEaseOut(markTime,markDuration,markTime1)
		}
	}
}
```

## 路径跟踪
### 获取修剪路径上的点坐标
```javascript
thePath = ;//路径
startEndValue = ;//开始点/结束点
offSetValue = ;//偏移量
var getTrimPathPoint = function(thePath,startEndValue,offSetValue) {
	//获取图层
	var i = 1,j = 0, theLayer = "";
	do {
		try {
			theLayer = thePath.propertyGroup(i);
			i = i + 1;
		} catch (err) {
			j = 1;
		}
	} while (j == 0)
	//获取结束点位置+偏移值
	var x=startEndValue/100 + offSetValue/360; 
	var y=x-Math.floor(x);
	return thePath.pointOnPath(y) + theLayer.toComp(transform.anchorPoint);//输出当前点位置 + 合成空间位置
}
getTrimPathPoint(thePath,startEndValue,offSetValue);
```

### 获取修剪路径上的点切线方向
```javascript
thePath = ;//路径
startEndValue = ;//开始点/结束点
offSetValue = ;//偏移量
var getTrimPathRotion = function(thePath,startEndValue,offSetValue) {
	//获取结束点位置+偏移值
	var x=startEndValue/100 + offSetValue/360; 
	var y=x-Math.floor(x);
	var tangent=thePath.tangentOnPath(y)//获取路径点tan值
	return 90 + value - radiansToDegrees(Math.atan2(tangent[0],tangent[1]));//转换tan到角度，输出当前角度值-路径角度值
}
getTrimPathRotion(thePath,startEndValue,offSetValue);
```
## 数组取整

### 数组四舍五入取整
```javascript
value = ;//此处输入数组
var arrayRound = function(value) {
	var arrayLength = value.length;
	var outputValue = value;
	for (i=0; i < arrayLength; i++){
		outputValue[i]=(Math.round(value[i]));
	}
	return outputValue;
}
arrayRound(value);
```

### 数组去除小数
```javascript
value = ;//此处输入数组
var arrayTrunc = function(value) {
	var arrayLength = value.length;
	var outputValue = value;
	for (i=0; i < arrayLength; i++){
		outputValue[i]=(Math.trunc(value[i]));
	}
	return outputValue;
}
arrayTrunc(value)
```

### 数组向上取整
```javascript
value = ;//此处输入数组
var arrayCeil = function(value) {
	var arrayLength = value.length;
	var outputValue = value;
	for (i=0; i < arrayLength; i++){
		outputValue[i]=(Math.ceil(value[i]));
	}
	return outputValue;
}
arrayCeil(value)
```

### 数组向下取整
```javascript
value = ;//此处输入数组
var arrayFloor = function(value) {
	var arrayLength = value.length;
	var outputValue = value;
	for (i=0; i < arrayLength; i++){
		outputValue[i]=(Math.floor(value[i]));
	}
	return outputValue;
}
arrayFloor(value);
```
## 获取图层变换
### 获取真实位置
```javascript
targetLayer = ;//输入图层
targetLayer.toWorld([0,0,0]);

```

### 获取真实旋转方向
```javascript
targetLayer = ;//输入图层
function getXRotion(){
	zVec = normalize(targetLayer.toWorldVec([0,0,1]));
	return radiansToDegrees(Math.atan2(-zVec[1], zVec[2]));
}
function getYRotion(){
	zVec = normalize(targetLayer.toWorldVec([0,0,1]));
	return radiansToDegrees(Math.asin(zVec[0]));
}
function getZRotion(){
	xVec = normalize(targetLayer.toWorldVec([1,0,0]));
	yVec = normalize(targetLayer.toWorldVec([0,1,0]));
	return radiansToDegrees(Math.atan2(-yVec[0], xVec[0]));
}
[getXRotion(),getYRotion(),getZRotion()];
```
### 计算两个物体在摄像机屏幕坐标系下的z轴距离
计算两个物体的前后距离，同时可用于判断物体前后关系<br />
New Bing AI写的表达式
```javascript
var A = ;//图层A
var B = ;//图层B
// 获取两个物体的世界坐标
var A_world = A.toWorld(A.anchorPoint);
var B_world = B.toWorld(B.anchorPoint);
// 获取摄像机的世界坐标和方向
var cam = thisComp.activeCamera;
var cam_world = cam.toWorld([0,0,0]);
var cam_dir = cam.toWorldVec([0,0,-1]);
// 计算两个物体在摄像机方向上的投影长度
var A_proj = dot(A_world - cam_world, cam_dir);
var B_proj = dot(B_world - cam_world, cam_dir);
//输出
var z_dist = A_proj - B_proj;
z_dist;
```
## 其他
### 在关键帧前随机颜色
用于颜色属性
```javascript
if (time < nearestKey(time).time){
posterizeTime(4);//设置帧数
seedRandom(index,timeless=false)
random([0,0,0,1],[1,1,1,1]);
}else{
	nearestKey(time).value;
}
```

<!-- 
MarkDownJS代码格式

```javascript

```
 -->
