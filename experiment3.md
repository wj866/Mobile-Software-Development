# 2025年夏季《移动软件开发》实验报告



<center>姓名：时伟杰  学号：23020007106</center>

| 姓名和学号？         | 时伟杰，23020007106              |
| -------------------- | -------------------------------- |
| 本实验属于哪门课程？ | 中国海洋大学25夏《移动软件开发》 |
| 实验名称？           | 实验3：微信小程序云开发          |



## **一、实验目标**

学习微信小程序云开发的基础知识。能够完成利用文本搜索的功能就好，图像识别、语音识别接口有时有问题，不强求。



## 二、实验步骤

1. 创建一个微信小程序，之前已经创建多次，这次不再重复

2. **[注册百度智能云并实名认证, 创建一个图像识别应用, 记录应用API KEY 和 SECRET KEY, 创建资源之后记得领取免费资源](https://gitee.com/link?target=https%3A%2F%2Fconsole.bce.baidu.com%2Fai%2F%3F_%3D%26fromai%3D1%23%2Fai%2Fimagerecognition%2Fapp%2Fcreate)**

   保存API Key和Secret Key

![image-20250901192646633](C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250901192646633.png)

3. 使用微信开发者工具创建一个云开发环境, 并复制环境ID

   ![云开发](https://s1.ax1x.com/2022/05/15/Og57Ae.png)

   ![环境ID](https://s1.ax1x.com/2022/05/15/Og55nK.png)

4. 进入微信开发者工具导入垃圾分类小程序项目, 注意我这里导入的是包含cloudfunctions,miniprogram,project.config.json的整个文件夹

![导入项目](https://s1.ax1x.com/2022/05/15/Og5RpR.png)

5. 添加百度API KEY \ SECRET 和 小程序appid, 云环境ID

![APPID](https://s1.ax1x.com/2022/05/15/Og56k4.png)

![云环境ID](https://s1.ax1x.com/2022/05/15/Og55nK.png)

![百度API KEY SECRET](https://s1.ax1x.com/2022/05/15/Og5ctJ.png)

6. 点击`cloudfuntions`文件夹展开子文件夹,依次右键点击展开的子文件夹并点击弹出的`上传并部署(不上传node_modules)`

![上传云函数](https://s1.ax1x.com/2022/05/15/Og5hX6.png)

7. 部署云数据库：点击小程序开发工具的云开发，点击数据库，创建集合trash, type，依次导入trash.json, type.json文件

![云开发按钮](https://s1.ax1x.com/2022/05/15/Og5o7D.png)

![数据库按钮](https://s1.ax1x.com/2022/05/15/Og5I0O.png)

![创建集合](https://s1.ax1x.com/2022/05/15/Og5r0U.png)

![导入文件1](https://s1.ax1x.com/2022/05/15/Og5DmT.png)

![导入文件2](https://s1.ax1x.com/2022/05/15/Og5gh9.png)

## 三、程序运行结果

<img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250901193640011.png" alt="image-20250901193640011" style="zoom:50%;" />



<img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250901193650141.png" alt="image-20250901193650141" style="zoom:50%;" />

<img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250901193704221.png" alt="image-20250901193704221" style="zoom:50%;" />

## 四、问题总结与体会

这个实验我学习了api接口的使用，还认识到了数据库的重要性。老师发的文档很详细，没遇到特别大的问题，跟着做一次就成功了。