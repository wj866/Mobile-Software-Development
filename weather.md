# 2025年夏季《移动软件开发》实验报告



<center>姓名：时伟杰  学号：23020007106</center>

| 姓名和学号？         | 时伟杰，23020007106                                          |
| -------------------- | ------------------------------------------------------------ |
| 本实验属于哪门课程？ | 中国海洋大学25夏《移动软件开发》                             |
| 实验名称？           | 实验2：天气查询小程序                                        |
| 博客地址？           | [OUC-2025移动软件开发-实验2-CSDN博客](https://blog.csdn.net/2301_79775855/article/details/150861033) |
| Github仓库地址？     | XXXXXXX                                                      |



## **一、实验目标**

1、学习使用快速启动模板创建小程序的方法；2、学习不使用模板手动创建小程序的方法。



## 二、实验步骤

依照[实验二文档](https://gitee.com/gaopursuit/mobile_software/raw/master/lab/lab2.pdf)所写，但是文档有些年代久远，并不是所有适用。

1.准备工作

①进入[和风平台](https://dev.qweather.com/)，先进行注册，再进入控制台，点击设置，复制API host，粘贴入记事本备用。

②点击项目管理，创建一个新的项目，随便输入项目名称，创建。之后创建一个项目凭据，凭据名称随便输入，复制API KEY，粘贴入记事本备用。

![image-20250826153206287](D:\桌面\image-20250826153206287.png)

③下载[图标库](https://icons.qweather.com/)，svg格式即可，不需要修改。

2.创建项目

还是JS基础版，创建即可。

①删除utils文件夹
②删除pages文件夹下的logs目录
③删除index.wxml和index.wxss中的全部代码
④删除index.js中的全部代码，并输入关键词page选择自动补全生成模板
⑤删除app.wxss中的全部代码
⑥删除app.js中的全部代码，并且输入关键词app自动补齐生成模板

创建images文件夹，将图标库全部复制进去。

3.编写代码如下

index.js 如下

```javascript
//index.js
Page({
  //页面的初始数据
  data: {
    region:['北京市','北京市','东城区'],
    now:''
  },
  changeRegion:function(e){
    this.setData({
        region:e.detail.value
    })
    this.getWeather();
},
getWeather:function(){
    var that=this;
    // 先获取城市ID
    wx.request({
    //-----------------下行需要填入你的API Host---------------------
        url: 'https://你的API Host/geo/v2/city/lookup', 
        data: {
            location: that.data.region, // 使用选择的区域
        },
        header: {
    //-----------------下行需要填入你的API KEY----------------------
            'X-QW-Api-Key': '你的API KEY'
        },
        success: function(res) {
            if (res.data.code === '200' && res.data.location.length > 0) {
                // 获取第一个城市的ID
                var locationId = res.data.location[0].id;
                // 请求天气数据
                wx.request({
    //-----------------下行需要填入你的API Host---------------------
                    url: 'https://你的API Host/v7/weather/now',
                    data: {
                        location: locationId
                    },
                    header: {
    //-----------------下行需要填入你的API KEY----------------------
                        'X-QW-Api-Key': '你的API KEY'
                    },
                    success: function(res){
                        console.log(res.data)
                        that.setData({now:res.data.now})
                    },
                });
            }
        },
    });
},
   //生命周期函数--监听页面加载
  onLoad: function (options) {
    this.getWeather();
  },
    
  //生命周期函数--监听页面初次渲染完成
  onReady: function () {
  },

   //生命周期函数--监听页面显示
  onShow: function () {
  },
    
   //生命周期函数--监听页面隐藏
  onHide: function () {
  },
  
   //生命周期函数--监听页面卸载
  onUnload: function () {
  },

   //页面相关事件处理函数--监听用户下拉动作
  onPullDownRefresh: function () {
  },

   //页面上拉触底事件的处理函数
  onReachBottom: function () {
  },

   //用户点击右上角分享
  onShareAppMessage: function () {
  }
})
```

index.wxml如下

```html
<!--index.wxml-->
<view class="container">
    <!--区域1：地区选择器-->
    <picker mode='region' bindchange='changeRegion'>
        <view>{{region}}</view>
    </picker>
    <!--区域2：文本-->
    <text>{{now.temp}}℃{{now.text}}</text>
    <!--区域3：图片-->
    <image src='/images/{{now.icon}}.svg'></image>
    <!--区域4：多行天气信息-->
    <view class='detail'>
        <view class="bar">
            <view class='box'>湿度</view>
            <view class='box'>气压</view>
            <view class='box'>能见度</view>
        </view>
        <view class="bar">
            <view class='box'>{{now.humidity}}%</view>
            <view class='box'>{{now.pressure}}hpa</view>
            <view class='box'>{{now.vis}}km</view>
        </view>
        <view class="bar">
            <view class='box'>风向</view>
            <view class='box'>风速</view>
            <view class='box'>风力</view>
        </view>
        <view class="bar">
            <view class='box'>{{now.windDir}}</view>
            <view class='box'>{{now.windSpeed}}km/h</view>
            <view class='box'>{{now.windScale}}级</view>
        </view>
    </view>
</view>
```

对index.wxml的解释：代码中的now.xxx是根据console中的now写的，如下图所示。

![image-20250826155723311](C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250826155723311.png)

index.wxss如下

```css
/**index.wxss**/
.container{
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;
}
.detail{
    display: flex;
    flex-direction: column;
    width: 100%;
}
.bar{
    display: flex;
    flex-direction: row;
    margin: 20rpx 0;
}
.box{
    width: 33.3%;
    text-align: center;
}
text{
    font-size: 80rpx;
    color: #3C5F81;
}
image{
    width: 220rpx;
}
```

app.json如下

```json
/**app.json**/
{
  "pages": [
    "pages/index/index"
  ],
  "window": {
      "navigationBarBackgroundColor": "#3883FA",
      "navigationBarTextStyle": "black",
      "navigationBarTitleText": "今日天气",
      "backgroundColor": "#eeeeee",
      "backgroundTextStyle": "light",
      "enablePullDownRefresh": false
  }
}
```

app.wxss如下

```css
/**app.wxss**/
.container {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  padding: 200rpx 0;
  box-sizing: border-box;
} 
```

## 三、程序运行结果

<img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250826160416386.png" alt="image-20250826160416386" style="zoom:50%;" />

<img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250826160500712.png" alt="image-20250826160500712" style="zoom:50%;" />

<img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250826160622759.png" alt="image-20250826160622759" style="zoom:50%;" />

## 四、问题总结与体会

描述实验过程中所遇到的问题，以及是如何解决的。有哪些收获和体会，对于课程的安排有哪些建议。

问题：

**API Host 和 API Key 的配置问题**
在初始阶段，由于未正确替换代码中的 `API Host` 和 `API Key`，导致无法正常获取天气数据。通过仔细阅读和风天气开发文档，确认了正确的接口地址和请求头格式，最终解决了该问题。

**数据绑定与渲染问题**
在编写 `index.wxml` 时，由于对 `data` 中 `now` 对象的结构理解不够清晰，部分字段名称写错，导致页面无法正确显示数据。通过查看控制台输出的 `res.data` 对象，逐步核对字段名称，最终完成了正确的数据绑定。

本次实验明显难了许多，原来的api也有一些变化，只能自己摸索和询问老师同学，解决问题之后也很有成就感。