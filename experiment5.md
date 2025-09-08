# 2025年夏季《移动软件开发》实验报告



<center>姓名：时伟杰  学号：23020007106</center>

| 姓名和学号？         | 时伟杰，23020007106                                          |
| -------------------- | ------------------------------------------------------------ |
| 本实验属于哪门课程？ | 中国海洋大学25夏《移动软件开发》                             |
| 实验名称？           | 实验5：第一个 HarmonyOS 应用                                 |
| 博客地址？           | [OUC-2025移动软件开发-实验5-CSDN博客](https://blog.csdn.net/2301_79775855/article/details/151316711?sharetype=blogdetail&sharerId=151316711&sharerefer=PC&sharesource=2301_79775855&spm=1011.2480.3001.8118) |
| Github仓库地址？     | [wj866/Mobile-Software-Development](https://github.com/wj866/Mobile-Software-Development) |



## **一、实验目标**

1、掌握如何构建 HarmonyOS应用；2、掌握应用程序包结构、资源文件的使用；3、掌握ArkTS的核心功能和语法等基础知识，为后续的应用开发奠定基础。



## 二、实验步骤

1. 工具准备：下载并安装[最新版DevEco Studio](https://developer.huawei.com/consumer/cn/download/)
2. 创建ArkTS工程：

①若首次打开DevEco Studio，请单击Create Project创建工程。如果已经打开了一个工程，请在菜单栏选择 File > New > Create Project来创建一个新工程。

②选择Application应用开发，选择模板Empty  Ability，单击Next进行下一步配置。

③进入配置工程界面，Compatible SDK表示兼容的最低API Version，此处以选择5.1.1(19)为例，其他参数保持默认设置即可。

![image-20250908105704243](C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250908105704243.png)

④单击Finish，工具会自动生成示例代码和相关资源，等待工程创建完成。

3. 构建页面

①第一个页面：在Project窗口，单击entry > src > main > ets > pages，打开Index.ets文件，填入以下代码

```eTS
// Index.ets
import { BusinessError } from '@kit.BasicServicesKit';
@Entry
@Component
struct Index {
  @State message: string = 'Hello World';
  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
        // 添加按钮，以响应用户onClick事件
        Button() {
          Text('Next')
            .fontSize(30)
            .fontWeight(FontWeight.Bold)
        }
        .type(ButtonType.Capsule)
        .margin({
          top: 20
        })
        .backgroundColor('#0D9FFB')
        .width('40%')
        .height('5%')
        // 跳转按钮绑定onClick事件，单击时跳转到第二页
        .onClick(() => {
          console.info(`Succeeded in clicking the 'Next' button.`)
          // 获取UIContext
          let uiContext: UIContext = this.getUIContext();
          let router = uiContext.getRouter();
          // 跳转到第二页
          router.pushUrl({ url: 'pages/Second' }).then(() => {
            console.info('Succeeded in jumping to the second page.')
          }).catch((err: BusinessError) => {
            console.error(`Failed to jump to the second page. Code is ${err.code},
message is ${err.message}`)
          })
        })
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

②第二个页面：在Project窗口，打开entry > src > main > ets，右键单击pages文件夹，选择 New > ArkTS File，命名为Second，单击回车键。

```eTS
// Second.ets
import { BusinessError } from '@kit.BasicServicesKit';
@Entry
@Component
struct Second {
  @State message: string = 'Hi there';
  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
        Button() {
          Text('Back')
            .fontSize(30)
            .fontWeight(FontWeight.Bold)
        }
        .type(ButtonType.Capsule)
        .margin({
          top: 20
        })
        .backgroundColor('#0D9FFB')
        .width('40%')
        .height('5%')
        // 返回按钮绑定onClick事件，单击按钮时返回到第一页
        .onClick(() => {
          console.info(`Succeeded in clicking the 'Back' button.`)
          // 获取UIContext
          let uiContext: UIContext = this.getUIContext();
          let router = uiContext.getRouter();
          try {
            // 返回第一页
            router.back()
            console.info('Succeeded in returning to the first page.')
          } catch (err) {
            let code = (err as BusinessError).code;
            let message = (err as BusinessError).message;
            console.error(`Failed to return to the first page. Code is ${code},
message is ${message}`)
          }
        })
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

打开Index.ets文件，单击预览器中的按钮进行刷新。

4. 真机演示

①将搭载HarmonyOS系统的真机与电脑连接。

②单击File > Project Structure... > Project > SigningConfigs界面勾选Support HarmonyOS和 Automatically generate signature，单击界面提示的Sign In，使用华为账号登录。等待自动签名完成后， 单击OK即可。如下图

![image-20250908110644260](C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250908110644260.png)

③在编辑窗口右上角的工具栏，单击按钮运行。

## 三、程序运行结果

真机演示的截图如下所示：

<img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250908110936234.png" alt="image-20250908110936234" style="zoom:50%;" />

<img src="C:\Users\m1585\AppData\Roaming\Typora\typora-user-images\image-20250908110950367.png" alt="image-20250908110950367" style="zoom:50%;" />

## 四、问题总结与体会

这次实验构建一个简单的具有页面跳转/返回功能的应用， 我能够快速了解工程目录的主要文件，熟悉HarmonyOS应用开发流程。

通过内容的学习和初步实践，我可以构建出首个HarmonyOS应用，掌握应用程序包结构、资 源文件的使用以及ArkTS的核心功能和语法等基础知识，为后续的应用开发奠定基础。