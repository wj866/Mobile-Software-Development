# 2025年夏季《移动软件开发》实验报告



<center>姓名：时伟杰  学号：23020007106</center>

| 姓名和学号？         | 时伟杰，23020007106                                          |
| -------------------- | ------------------------------------------------------------ |
| 本实验属于哪门课程？ | 中国海洋大学25夏《移动软件开发》                             |
| 实验名称？           | 实验1：第一个微信小程序                                      |
| 博客地址？           | [时伟杰博客](https://blog.csdn.net/2301_79775855/article/details/150781261?spm=1001.2014.3001.5502) |
| Github仓库地址？     | [时伟杰github](https://github.com/wj866/Mobile-Software-Development) |

（备注：将实验报告发布在博客、代码公开至 github 是 **加分项**，不是必须做的）



## **一、实验目标**

1、学习使用快速启动模板创建小程序的方法；2、学习不使用模板手动创建小程序的方法。



## 二、实验步骤

1.进入https://mp.weixin.qq.com/注册小程序开发账号

2.将小程序信息完善

![image-20250825182255813](C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250825182255813.png)

3.下载安装微信开发者工具

![image-20250825194544597](C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250825194544597.png)

4.自动自己的第一个小程序

选择好目录和AppID，选择js基础班这一框架

![image-20250825194647596](C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250825194647596.png)

结果如图所示

<img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250825194920031.png" alt="image-20250825194920031" style="zoom:50%;" />

5.手动创建小程序

①删除utils文件夹
②删除pages文件夹下的logs目录
③删除index.wxml和index.wxss中的全部代码
④删除index.js中的全部代码，并输入关键词page选择自动补全生成模板
⑤删除app.wxss中的全部代码
⑥删除app.js中的全部代码，并且输入关键词app自动补齐生成模板

小程序默认导航栏是⿊底⽩字的效果,可以通过在app.json中对window 属性进⾏重新配置来⾃定义导航栏效果。代码如下：

```json
{
  "pages": [
    "pages/index/index"
  ],
  "window": {
    "navigationBarBackgroundColor": "#663399",
    "navigationBarTitleText": "手动创建第一个小程序",
    "navigationBarTextStyle": "white"
  }
}
```

上述代码可以更改导航栏背景⾊为紫色、字体为白色。

微信头像组件、微信昵称组件、按钮组件按照以下代码更改。在index.wxml⻚⾯修改组件的代码,为其追加获取用户信息事件。（其中open-type= getUserlnfo表示激活获取微信⽤户信息功能,然后使用bindgetuserinfo表 示获得的数据将传递给自定义函数getMyInfo,该名称可以自定义。）

```html
<view class = "container">
    <image src = '{{src}}' mode = 'widthFix'></image>
    <text>{{name}}</text>
    <button open-type='getUserInfo'bindgetuserinfo = 'getMyInfo'> 点击获取头像和昵称 
    </button>
</view>
```

```css
.container{
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;
}
image {
    width: 300rpx;
    border-radius: 50%;
}
text {
    font-size: 50rpx;
}
```

在index.js⻚⾯的Page()内部追加getMyInfo函数和onLoad函数。

```javascript
Page({
//页面的初始数据
  data: {
    src: '/images/logo.jpg',
    name: 'Hello World'
  },
// 获取用户信息
getMyInfo: function(e) {
    wx.getUserProfile({
      desc: '展示用户信息', 
      success: (res) => {
        console.log(res)
        this.setData({
          src: res.userInfo.avatarUrl,
          name: res.userInfo.nickName
        })
      }
    })
  }
})
```

至此，实验1结束。

## 三、程序运行结果

<img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250825200259872.png" alt="image-20250825200259872" style="zoom:50%;" />

<img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250825200314110.png" alt="image-20250825200314110" style="zoom:50%;" />

## 四、问题总结与体会

通过本次实验，我初步掌握了微信小程序的开发流程，包括环境配置、项目创建、组件使用和API调用。在手动创建小程序的过程中，遇到了导航栏配置、用户信息授权和页面布局等问题，通过查阅官方文档和调试分析逐一解决了这些困难。

- 问题：初始布局使用`space-around`导致元素分布不均匀，与预期效果不符。
- 解决：将`justify-content: space-around`改为`justify-content: center`并添加适当的间距，实现垂直居中布局。

通过这次实验，我不仅学会了如何创建小程序，更重要的是培养了独立解决问题的能力，对今后的学习和开发都有很大帮助。