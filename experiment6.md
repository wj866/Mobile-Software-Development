# 2025年夏季《移动软件开发》实验报告



<center>姓名：时伟杰  学号：23020007106</center>

| 姓名和学号？         | 时伟杰，23020007106              |
| -------------------- | -------------------------------- |
| 本实验属于哪门课程？ | 中国海洋大学25夏《移动软件开发》 |
| 实验名称？           | 实验3：微信小程序云开发          |
| 博客地址？           | XXXXXXX                          |
| Github仓库地址？     | XXXXXXX                          |



## **一、实验目标**

学习微信小程序云开发的基础知识。能够完成利用文本搜索的功能就好，图像识别、语音识别接口有时有问题，不强求。



## 二、实验步骤

1. 准备工作：创建js基础版模板，此处省略。添加images文件夹存放图片；创建js文件data.js存储数据信息。

   ```
   ex6/
   ├── .eslintrc.js
   ├── app.js
   ├── app.json
   ├── app.wxss
   ├── project.config.json
   ├── project.private.config.json
   ├── sitemap.json
   ├── images/ 
   │   ├── level01.png
   │   ├── level02.png
   │   ├── level03.png
   │   ├── level04.png
   │   └── icons/
   │       ├── ice.png
   │       ├── stone.png
   │       ├── pig.png
   │       ├── box.png
   │       └── bird.png
   ├── pages/
   │   ├── index/
   │   │   ├── index.js
   │   │   ├── index.json
   │   │   ├── index.wxml
   │   │   └── index.wxss
   │   └── game/
   │       ├── game.js
   │       ├── game.json
   │       ├── game.wxml
   │       └── game.wxss
   └── utils/
       └── data.js
   ```

2. 代码如下

**game.js**

```js
// pages/game/game.js
var data = require('../../utils/data.js')

var map=[
  [0,0,0,0,0,0,0,0],
  [0,0,0,0,0,0,0,0],
  [0,0,0,0,0,0,0,0],
  [0,0,0,0,0,0,0,0],
  [0,0,0,0,0,0,0,0],
  [0,0,0,0,0,0,0,0],
  [0,0,0,0,0,0,0,0],
  [0,0,0,0,0,0,0,0]
]

var box=[
  [0,0,0,0,0,0,0,0],
  [0,0,0,0,0,0,0,0],
  [0,0,0,0,0,0,0,0],
  [0,0,0,0,0,0,0,0],
  [0,0,0,0,0,0,0,0],
  [0,0,0,0,0,0,0,0],
  [0,0,0,0,0,0,0,0],
  [0,0,0,0,0,0,0,0]
]

var w = 40
var row = 0
var col = 0

Page({

  /**
   * 页面的初始数据
   */
  data: {

  },

  isWin:function(){
    for (var i = 0; i < 8;i++){
      for (var j = 0;j<8;j++){
        if(box[i][j] == 4 && map[i][j] !=3){
          return false
        } 
      }
    }
    return true
  },

  checkWin:function(){
    if(this.isWin()){
      wx.showModal({
        title: '恭喜',
        content: '游戏成功',
        showCancel:false
      })
    }
  },

  up:function(){
if (row > 0){
  if (map[row-1][col] != 1&& box[row-1][col]!=4){
    row = row-1
  }
  else if(box[row-1][col] == 4){
    if(row-1 > 0){
      if(map[row - 2][col]!=1&&box[row-2][col]!=4){
        box[row-2][col] = 4
        box[row-1][col] = 0
        row=row-1
      }
    }
  }
  this.drawCanvas()
  this.checkWin()
}
  },

  
  down:function(){
    if (row < 7){
      if (map[row+1][col] != 1&& box[row+1][col]!=4){
        row = row+1
      }
      else if(box[row+1][col] == 4){
        if(row+1 < 7){
          if(map[row + 2][col]!=1&&box[row+2][col]!=4){
            box[row+2][col] = 4
            box[row+1][col] = 0
            row=row+1
          }
        }
      }
      this.drawCanvas()
      this.checkWin()
    }
      },

      
  left:function(){
    if (col > 0){
      if (map[row][col-1] != 1&& box[row][col-1]!=4){
        col = col-1
      }
      else if(box[row][col-1] == 4){
        if(col-1 > 0){
          if(map[row][col-2]!=1&&box[row][col-2]!=4){
            box[row][col-2] = 4
            box[row][col-1] = 0
            col=col-1
          }
        }
      }
      this.drawCanvas()
      this.checkWin()
    }
      },

      left:function(){
        if (col > 0){
          if (map[row][col-1] != 1&& box[row][col-1]!=4){
            col = col-1
          }
          else if(box[row][col-1] == 4){
            if(col-1 > 0){
              if(map[row][col-2]!=1&&box[row][col-2]!=4){
                box[row][col-2] = 4
                box[row][col-1] = 0
                col=col-1
              }
            }
          }
          this.drawCanvas()
          this.checkWin()
        }
          },

          right:function(){
            if (col < 7){
              if (map[row][col+1] != 1&& box[row][col+1]!=4){
                col = col+1
              }
              else if(box[row][col+1] == 4){
                if(col+1 < 7){
                  if(map[row][col+2]!=1&&box[row][col+2]!=4){
                    box[row][col+2] = 4
                    box[row][col+1] = 0
                    col=col+1
                  }
                }
              }
              this.drawCanvas()
              this.checkWin()
            }
              },

 initMap:function(level){
  let mapData = data.maps[level]
  for (var i = 0;i < 8;i++){
  for (var j = 0;j<8;j++){
    box[i][j] = 0
    map[i][j] = mapData[i][j]
    if(mapData[i][j] == 4){
      box[i][j] = 4
      map[i][j] = 2
    }else if(mapData[i][j] == 5){
      map[i][j] = 2
      row = i
      col = j
    }
  }
  }
 },

 drawCanvas:function(){
   let ctx = this.ctx
   ctx.clearRect(0,0,320,320)
   for (var i = 0;i < 8;i++){
    for (var j = 0;j<8;j++){
     let img = 'ice'
     if(map[i][j] == 1){
       img = 'stone'
     }else if(map[i][j] == 3){
       img = 'pig'
     }

     ctx.drawImage('/images/icons/' + img + '.png',j*w,i*w,w,w)
     if(box[i][j] == 4){
       ctx.drawImage('/images/icons/box.png',j*w,i*w,w,w)
     }
    }
  }
  ctx.drawImage('/images/icons/bird.png',col*w,row*w,w,w)
  ctx.draw()
 },


  restartGame:function(){
  this.initMap(this.data.level-1)
  this.drawCanvas()
  },

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad(options) {
  let level = options.level
  this.setData({
    level:parseInt(level) + 1
  })
  this.ctx = wx.createCanvasContext('myCanvas')
  this.initMap(level)
  this.drawCanvas()
},

  /**
   * 生命周期函数--监听页面初次渲染完成
   */
  onReady() {

  },

  /**
   * 生命周期函数--监听页面显示
   */
  onShow() {

  },

  /**
   * 生命周期函数--监听页面隐藏
   */
  onHide() {

  },

  /**
   * 生命周期函数--监听页面卸载
   */
  onUnload() {

  },

  /**
   * 页面相关事件处理函数--监听用户下拉动作
   */
  onPullDownRefresh() {

  },

  /**
   * 页面上拉触底事件的处理函数
   */
  onReachBottom() {

  },

  /**
   * 用户点击右上角分享
   */
  onShareAppMessage() {

  }
})
```

game.json如下

```html
<!--pages/game/game.wxml-->
<view class = 'container'>
  <view class = 'title'>第{{level}}关</view>
  
  <canvas canvas-id='myCanvas'></canvas>
  
  <view class = 'btnBox'>
    <button type = 'warn' bindtap = 'up'>↑</button>
  <view>
    <button type = 'warn' bindtap = 'left'>←</button>
    <button type = 'warn' bindtap = 'down'>↓</button>
    <button type = 'warn' bindtap = 'right'>→</button>
  </view>
  </view>

  <button type = 'warn'bindtap='restartGame'>重新开始</button>
</view>
  

```

game.wxss如下

```css
/* pages/game/game.wxss */
canvas{
  border:1rpx solid;
  width: 320px;
  height: 320px;
}

.btnBox{
  display: flex;
  flex-direction: column;
  align-items: center;
}

.btnBox view{
  display: flex;
  flex-direction: row;
}

.btnBox button{
  width: 90rpx;
  height: 90rpx;
}

button{
  margin:10rpx;
}
```

index.js如下

```js
Page({
  /**
   * 页面的初始数据
   */
  data: {
    levels:[
      'level01.png',
      'level02.png',
      'level03.png',
      'level04.png'
    ]
  },

  chooseLevel:function(e){
  let level = e.currentTarget.dataset.level
  wx.navigateTo({
    url: '../game/game?level=' + level
  })
  },

  /**
   * 生命周期函数--监听页面加载
   */
  onLoad: function (options) {
    
  },

  /**
   * 生命周期函数--监听页面初次渲染完成
   */
  onReady: function () {
    
  },

  /**
   * 生命周期函数--监听页面显示
   */
  onShow: function () {
    
  },

  /**
   * 生命周期函数--监听页面隐藏
   */
  onHide: function () {
    
  },

  /**
   * 生命周期函数--监听页面卸载
   */
  onUnload: function () {
    
  },

  /**
   * 页面相关事件处理函数--监听用户下拉动作
   */
  onPullDownRefresh: function () {
    
  },

  /**
   * 页面上拉触底事件的处理函数
   */
  onReachBottom: function () {
    
  },

  /**
   * 用户点击右上角分享
   */
  onShareAppMessage: function () {
    
  }
})
```

index.wxml如下

```html
<view class='container'>
  <!-- 标题 -->
  <view class='title'>游戏选关</view>
  <!-- 关卡列表 -->
  <view class='levelBox'>
    <view class='box' wx:for='{{levels}}' wx:key='levels{{index}}'bindtap='chooseLevel'data-level='{{index}}'>
      <image src='/images/{{item}}'></image>
      <text>第{{index+1}}关</text>
    </view>
  </view>
</view>
```

index.wxss如下

```css
.levelBox{
  width: 100%;
}

.box{
  width: 50%;
  float:left;
  margin:20rpx 0;
  display: flex;
  flex-direction: column;
  align-items: center;
}

image{
  width: 300rpx;
  height: 300rpx;
}
```

data.js如下

```js
// 地图数据map1-map4
// 地图数据：1为墙，2为路，3为终点，4为箱子，5为人物，0墙的外围

// 关卡一
var map1=[
  [0,1,1,1,1,1,0,0],
  [0,1,2,2,1,1,1,0],
  [0,1,5,4,2,2,1,0],
  [1,1,1,2,1,2,1,1],
  [1,3,1,2,1,2,2,1],
  [1,3,4,2,2,1,2,1],
  [1,3,2,2,2,4,2,1],
  [1,1,1,1,1,1,1,1]
]
// 关卡二
var map2=[
  [0,0,1,1,1,0,0,0],
  [0,0,1,3,1,0,0,0],
  [0,0,1,2,1,1,1,1],
  [1,1,1,4,2,4,3,1],
  [1,3,2,4,5,1,1,1],
  [1,1,1,1,4,1,0,0],
  [0,0,0,1,3,1,0,0],
  [0,0,0,1,1,1,0,0]
]
// 关卡三

var map3=[
  [0,0,1,1,1,1,0,0],
  [0,0,1,3,3,1,0,0],
  [0,1,1,2,3,1,1,0],
  [0,1,2,2,4,3,1,0],
  [1,1,2,2,5,4,1,1],
  [1,2,2,1,4,4,2,1],
  [1,2,2,2,2,2,2,1],
  [1,1,1,1,1,1,1,1]
]
// 关卡四
var map4=[
  [0,1,1,1,1,1,1,0],
  [0,1,3,2,3,3,1,0],
  [0,1,3,2,4,3,1,0],
  [1,1,1,2,2,4,1,1],
  [1,2,4,2,2,4,2,1],
  [1,2,1,4,1,1,2,1],
  [1,2,2,2,5,2,2,1],
  [1,1,1,1,1,1,1,1]
]
module.exports={
  maps:[map1,map2,map3,map4]
}
```

.eslintrc.js

```js
/*
 * Eslint config file
 * Documentation: https://eslint.org/docs/user-guide/configuring/
 * Install the Eslint extension before using this feature.
 */
module.exports = {
  env: {
    es6: true,
    browser: true,
    node: true,
  },
  ecmaFeatures: {
    modules: true,
  },
  parserOptions: {
    ecmaVersion: 2018,
    sourceType: 'module',
  },
  globals: {
    wx: true,
    App: true,
    Page: true,
    getCurrentPages: true,
    getApp: true,
    Component: true,
    requirePlugin: true,
    requireMiniProgram: true,
  },
  // extends: 'eslint:recommended',
  rules: {},
}
```

app.json：

```json
{
  "pages": [
    "pages/index/index",
    "pages/game/game"

  ],
  "window": {
    "backgroundTextStyle":"light",
    "navigationBarTextStyle": "white",
    "navigationBarTitleText": "推箱子小游戏",
    "navigationBarBackgroundColor": "#E64340"
  }
}
```

app.wxss如下：

```css
/* 页面容器样式 */
.container{
  height: 100vh;
  color: #E64340;
  font-weight: bold;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
}
/* 顶端标题样式 */
.title{
  font-size: 18pt;
}
```

## 三、程序运行结果

<img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250908143417976.png" alt="image-20250908143417976" style="zoom:50%;" />

<img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250908143425085.png" alt="image-20250908143425085" style="zoom:50%;" />



<img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250908143438476.png" alt="image-20250908143438476" style="zoom:50%;" />

## 四、问题总结与体会

这次实验实现了推箱子小游戏，根据教程做就可以成功。