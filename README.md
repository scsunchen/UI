响应式用户交互组件库UI
======
## demo:[最新版](http://bh-lay.github.io/UI/)
## 下载：只需要一个文件，多神奇 [dialog.js](src/dialog.js)
# 一、简介

## 1.1、UI是什么?
UI是前端公用的视觉交互（user interface 、 user interaction）类公用组建，用于和用户间的对话及动态界面展示。

## 1.2、UI目前有哪儿些内容？

* 目前有虚拟弹层、弹框、提示信息、确认对话、列表选择等功能
* 支持对象化事件的调用
* 支持窗体自由`拖拽`
* 支持`自定义位置`，方便控制对象在页面中的呈现
* 对象被注销有`回调支持`，方便确认对象状态
* 不依赖任何库，随拿随用
* 动画使用CSS3实现，IE无动画效果（策略问题）

## 1.3、问题反馈
在使用中有任何问题，欢迎反馈给我，可以用以下联系方式跟我交流

* 邮件：bh-lay#126.com
* github: [http://github.com/bh-lay](http://github.com/bh-lay)
* weibo: [@剧中人](http://weibo.com/bhlay)


# 二、如何使用

## 2.0 基本配置
### UI.config.gap
为pop弹框配置页面显示的边界（默认值均为零），可用在弹框展开时与拖动处理时限定自身位置。

### UI.config.zIndex
设置组件在页面中的**z-index**层级

### demo
```javascript
//设置边界
//top right bottom left
UI.config.gap('top',100);
//设置层级
UI.config.zIndex(5000);
```

## 2.1 UI.pop 弹框
用途比较广泛，可自定义尺寸位置、是否需要标题、是否显示蒙层、确认按钮（是否需要及按钮文字）等。
### param 传入参数
 * *Object* **param** 参数对象
 * *String* [**param.title**] 弹框标题
 * *String* **param.html** 弹框内容
 * *String* [**param.width**] 弹框宽度
 ~~* *String* [**param.height**] 弹框高度（推荐根据内容自适应）~~
 * *String* [**param.top**] 弹框与页面顶部距离
 * *String* [**param.left**] 弹框与页面左侧距离
 * *Boolean* [**param.mask**] 是否显示蒙层（默认不显示）
 * *Boolean* [**param.easyClose**] 点击空白或按下esc，关闭自己
 * *Function* [**param.init**] 对象构建完成时的回调（主要是动画）
 * *Object|Function* [**param.confirm**] 使用对话方式（详细定义或只定义回调）
 * *Array* [**param.confirm.btns**] 按钮自定义名称
 * *Function* [**param.confirm.callback**] 确定时的回调方法

### returns 返回值
 * *Object* **pop** 弹框对象
 * *Object* **pop.node** 弹框所属DOM
 * *Object* **pop.cntDom** 弹框内容部分DOM
 * *Function* **pop.destroy** 关闭弹框的方法
 * *Function* **pop.adapt** 自动调整对象在页面中的位置（用于弹框内容发生变化时）
 
### demo
```javascript
var pop = UI.pop({
  'title' : '我的弹框',
  'top' : 200,
  'left' : '600',
  'html' : 'this is html'
});
UI.pop({
  'title' : '我是自定义按钮的弹框',
  'confirm' : {
    'btns' : ['好的','不干'],
    'callback' : function(){
      alert(1);
    }
  },
//  'confirm' : function(){
//    alert(2);
//  }
});
```

## 2.2、 UI.confirm 确认对话框
询问用户是否进行该操作。
### param 传入参数
 * *Object* **param** 参数对象
 * *String* **param.text** 提示内容
 * *Array* [**param.btns**] 按钮自定义名称
 * *String* [**param.mask**] 是否显示蒙层(默认显示)
 * *Function* [**param.callback**] 确定时的回调方法
 * *Function* [**param.init**] 对象构建完成时的回调（主要是动画）

### returns 返回值
 * *Object* **confirm**
 * *Object* **confirm.node** 弹框所属DOM
 * *Function* **confirm.destroy** 关闭弹框的方法

### demo
```javascript
UI.confirm({
  'text' : '请我吃饭吧！',
  'btns' : ['好的呀','不愿意'],
  'callback' : function(){
    alert('你是好人！');
  }
});
```

## 2.3、 UI.plane 虚拟弹层
没有样式，页面中只能同时存在一个plane实例化后的对象，点击自己以外的DOM，就会关掉自己，生命体征较弱的屌丝

## 2.4、UI.select 选择组件
展示一组待选项，供用户选择，移动端样式仿IOS原生ActionSheet组件（web版样式尚未完成）

### param 传入参数
 * *Array* **list** 提示内容列表
 * *Array* **list[0]** 提示内容选项
 * *String* **list[0][0]** 提示内容选项标题
 * *Function* **list[0][1]** 提示内容选项被选择后的回调
 * *Object* [**param**] 参数对象
 * *String* [**param.title**] 标题
 * *String* [**param.intro**] 提示文字
 * *Function* [**param.init**] 对象构建完成时的回调（主要是动画）

### returns 返回值
 * *Object* **select** select对象
 * *Object* **select.node** select所属DOM

### demo
```javascript
UI.select([
	['劈脸呼你',function(){
		UI.prompt('脸好疼');
	}],
	['一刀捅死你',function(){
		UI.prompt('啊，我死了');
	}],
	['滚一边去',function(){
		UI.prompt('滚远了');
	}]
],{
	'title' : '侬想组啥？',
	'intro' : '来一帮人，想打架么'
});
```
## 2.5、UI.prompt 提示信息
### param 传入参数
 * *String* **text** 提示内容
 * *Number* [**time**] 默认为1300ms，0为不自动关闭

### returns 返回值
 * *Object* **prompt**
 * *Object* **prompt.node** prompt所属DOM
 * *Function* **prompt.tips** 为prompt设置内容
 接收text 和 time两个参数，关闭时间处理同UI.prompt主方法
 * *Function* **prompt.destroy** 关闭prompt

### demo
```javascript
//默认时间
    UI.prompt('操作失败');
//指定时间
    UI.prompt('操作失败',2400);
//主动控制
    var a = UI.prompt('正在发送',0);
    a.tips('发送成功'，1200);
    
    var b = UI.prompt('请等待……',0);
    b.destroy();
```
## 2.6、UI.cover 全屏浮层
覆盖整个页面的浮层，目前对关闭的设计有点生硬，欢迎提出宝贵意见。

### param 传入参数
 * *Object* **param** 参数对象
 * *String* **param.html** 弹层内容
 * *Function* [**param.init**] 对象构建完成时的回调（主要是动画）

### returns 返回值
 * *Object* **cover** cover对象
 * *Object* **cover.node** cover所属DOM
 * *Function* **cover.destroy** 关闭cover

### demo
```javascript
UI.cover({
    'html' : '<div>....</div>'
});
```

## 2.7、UI.ask 输入弹层
用在需要用户输入数据时，以弹层的形式出现。

### param 传入参数
 * *String* **text** 引导信息
 * *Function* [**callback**] 点击确定时的回调
   默认会在掉用后关掉弹层，方法内return false会阻止关闭动作
 * *Function* [**param.init**] 对象构建完成时的回调（主要是动画）

### returns 返回值
 * *Object* **ask** ask对象
 * *Object* **ask.node** ask所属DOM
 * *Function* **ask.setValue** 设置内容
 * *Function* **ask.destroy** 关闭ask对象

### demo
```javascript
UI.ask('你今年多大了？',function(year){
	if(year == +year){
		if(year > 30){
			UI.prompt('都' + year + '岁了啊，这么老啊！');
		}else if(year > 17){
			UI.prompt('干柴烈火的年纪哦！');
		}else{
			UI.prompt('回家玩儿去！');
		}
	}else{
		UI.prompt('写个数字会死啊!');
		return false
	}
});
```
