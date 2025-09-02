# 2025年夏季《移动软件开发》实验报告



<center>姓名：时伟杰  学号：23020007106</center>

| 姓名和学号？         | 时伟杰，23020007106                                          |
| -------------------- | ------------------------------------------------------------ |
| 本实验属于哪门课程？ | 中国海洋大学25夏《移动软件开发》                             |
| 实验名称？           | 实验4：媒体API之口述校史                                     |
| 博客地址？           | [OUC-2025移动软件开发-实验4-CSDN博客](https://blog.csdn.net/2301_79775855/article/details/151101764?sharetype=blogdetail&sharerId=151101764&sharerefer=PC&sharesource=2301_79775855&spm=1011.2480.3001.8118) |
| Github仓库地址？     | [时伟杰](https://github.com/wj866/Mobile-Software-Development) |



## **一、实验目标**

1、掌握视频API的操作方法；2、掌握如何发送随机颜色的弹幕。



## 二、实验步骤

1. 准备步骤

①删除utils文件夹

②删除pages文件夹下的logs目录

③删除index.wxml和index.wxss中的全部代码

④删除index.js中的全部代码，并输入关键词page选择自动补全生成模板

⑤删除app.wxss中的全部代码

⑥删除app.js中的全部代码，并且输入关键词app自动补齐生成模板

⑦[下载](https://gaopursuit.oss-cn-beijing.aliyuncs.com/2022/images_play.zip )play.png,导入images文件夹

2. 编写代码

index.js代码如下

```js
function getRandomColor() {
  let rgb=[]
  for(let i = 0;i<3;++i){
    let color = Math.floor(Math.random()*256).toString(16)
    color = color.length == 1?'0'+color:color
    rgb.push(color)
  }
  return '#'+rgb.join('')
}
 
Page({
  playVideo:function(e){
    this.videoCtx.stop()
    this.setData({
      src:e.currentTarget.dataset.url
    })
    this.videoCtx.play()
  },
  data: {
    danmuTxt:'',
    list: [
      {
        id: '299371',
        title: '杨国宜先生口述校史实录',
        videoUrl: 'http://arch.ahnu.edu.cn/__local/6/CB/D1/C2DF3FC847F4CE2ABB67034C595_025F0082_ABD7AE2.mp4?e=.mp4'
      },
      {
        id: '299396',
        title: '唐成伦先生口述校史实录',
        videoUrl: 'http://arch.ahnu.edu.cn/__local/E/31/EB/2F368A265E6C842BB6A63EE5F97_425ABEDD_7167F22.mp4?e=.mp4'
      },
      {
        id: '299378',
        title: '倪光明先生口述校史实录',
        videoUrl: 'http://arch.ahnu.edu.cn/__local/9/DC/3B/35687573BA2145023FDAEBAFE67_AAD8D222_925F3FF.mp4?e=.mp4'
      },
      {
        id: '299392',
        title: '吴仪兴先生口述校史实录',
        videoUrl: 'http://arch.ahnu.edu.cn/__local/5/DA/BD/7A27865731CF2B096E90B522005_A29CB142_6525BCF.mp4?e=.mp4'
      }
    ]
  },
  getDanmu:function(e){
    this.setData({
      danmuTxt:e.detail.value
    })
  },
  sendDanmu:function(e){
    let text = this.data.danmuTxt;
    this.videoCtx.sendDanmu({
      text:text,
      color:getRandomColor()
    })
  },
  /**
   * 生命周期函数--监听页面加载
   */
 
  onLoad: function (options) {
    this.videoCtx = wx.createVideoContext('myVideo')
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

```html
<!-- index.wxml-->
<video id="myVideo" src="{{src}}" controls enable-danmu-btn></video>
<view class="danmuArea">
  <input type="text" placeholder="请输入弹幕内容" bindinput="getDanmu" />
  <button bindtap="sendDanmu">发送弹幕</button>
</view>

<view class="videoList">
  <view
    class="videoBar"
    wx:for="{{list}}"
    wx:key="video{{index}}"
    data-url="{{item.videoUrl}}"
    bindtap="playVideo"
  >
    <image src="/images/play.png"></image>
    <text>{{item.title}}</text>
  </view>
</view>
```

index.wxss代码如下

```css
 video{
  width : 100% ;
}
.danmuArea{
  display: flex;
  flex-direction: row;
}
input{
  border: 1 rpx soild #987938;
  flex-grow: 1;
  height: 100rpx;
}
button{ 
  color: white;
  background-color: #987938;
}
.videoList{
  width: 100%;
  min-height: 400 rpx;
}
.videoBar{
  width: 95%;
  display: flex;
  flex-direction: row;
  border-bottom: 1rpx soild #987938;
  margin: 10 rpx;
}
image{
  width: 50rpx ;
  height: 50rpx ;
  margin: 50rpx;
}
text{
  font-size: 45 rpx;
  color:#987938;
  flex-grow:1;
  margin: 20rpx;
}
```

.eslintrc.js代码如下

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

app.json代码如下

```json
{
  "pages": [
    "pages/index/index"
  ],
  "window": {
    "navigationBarTitleText": "口述校史",
    "navigationBarBackgroundColor": "#987938"
  }
}
```

## 三、程序运行结果

<img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250902091231356.png" alt="image-20250902091231356" style="zoom:50%;" /><img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250902091434721.png" alt="image-20250902091434721" style="zoom: 50%;" />

## 四、问题总结与体会

通过本次实验，我了解了微信小程序视频API的使用方法，包括视频播放、暂停、切换等基本操作，以及发送弹幕的实现过程。实验过程中我通过将getRandomColor函数定义在Page外部，确保了随机颜色生成功能的正常调用。通过这次实验，我学会了技术实现，培养了我发现问题、分析问题和解决问题的能力。