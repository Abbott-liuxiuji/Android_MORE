# android 系统机构
***
### 1、Android是什么？

首先，就像Android开源和兼容性技术负责人Dan Morrill在Android开发手册兼容性部分所解释的，“Android并不是传统的Linux风格的一个规范或分发版本，也不是一系列可重用的组件集成，Android是一个用于连接设备的软件块。”

![androidwhy1](/image/androidwhy1.png)

**Linux：**

所有东西的底层是一个稳定的保持更新的Linux内核（我现在用的Nexus手机所用的就是2.6.32版的内核），以及我们精心打造的能源管理组件；当然还有将它们整合至上层Linux代码的扩展和公共组件。

**Dalvik：**

Android另一个重要的部分，包括虚拟机和一组重要的运行环境。它的设计非常巧妙，是个很好的一个手机终端的底层应用。

**代码如何生成？**

Dalvik虚拟机只执行.dex的可执行文件。当Java程序通过编译，最后还需要通过SDK中的工具转化成.dex格式才能在虚拟机上执行。

我需要强调的是，Android应用本身就可视作可在平台上运行并调用APIs的代码，所以对代码如何生成不需特别看重。

**特别的Apps：**

在图中有些基于Dalvik虚拟机的Apps看起来像是Android的一部分，其实是由Google提供，这些应用包括Dialer、 Contact、Calendar、Gmail和Chat等。它们中的绝大部分是开源并可复用的。只有少部分例外，比如Google Maps和Android Market.

**开源那些事：**

在下面的图中，绿色的大部分组件是基于Apache许可证开源，其余基于GPL、LGPL和BSD。

![androidwhy2](/image/androidwhy2.png)

**Android框架**

在Android开发者网（developer.android.com)

![androidwhy3](/image/androidwhy3.png)

**标准库**

在这里“标准”是指“开发者在开源环境中一般可以使用的”。

**App里面是什么**

一个Android App包含在一个我们称之为APK的压缩文件夹中，APK并没有什么可说的，需要注意的是Android Manifest——介于App和Android System的接口。（大多数应用是基于Dalvik的，我指的是除了游戏之外的应用。游戏开发者通常希望用C/C++来编写，排斥使用虚拟机，所以他们可以通过Andriod NDK来开发。）

![androidwhy4](/image/androidwhy4.png)

![androidwhy5](/image/androidwhy5.png)
