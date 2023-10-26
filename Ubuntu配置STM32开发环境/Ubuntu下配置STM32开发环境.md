# Ubuntu下配置STM32开发环境(VSCode + STM32CubeMX)

## 1.工具准备
VSCode

STM32CubeMX

OpenOCD

gcc-arm-none-eabi编译器
## 2.步骤-以点亮板载LED为例
- ## OpenOCD配置


- （1）打开STM32CubeMX，单击FILE-New Project(或者图中选项)
![img1](https://img-blog.csdnimg.cn/23a4653015b0473da560fb900583b45c.png)

- （2）弹出芯片选择界面，在Commercial搜索框输入F103C8T6右下方会自动出现STM32F103C8T6，点击选择，然后点Start Project
![img1](https://img-blog.csdnimg.cn/b82395f801d04d14bdc28b55f9a4ef2d.png)

- （3）进入配置界面后单击System Core（系统核心） → SYS → Debug → Serial Wire（这个是调试模式，如果不选Serial Wire则可能会使得无法使用Stlink或Jlink下载，如果你是用串口线下载，不调试，不选也没关系）。

    （图片仅供示意，忽略右边的芯片设置）
![img1](https://img-blog.csdnimg.cn/7e29a57ebca148f7bdcdaab281cecafd.png)

- （4）单击System Core（系统核心） → RCC（配置晶振） → High speed Clock(HSE)（高速晶振）→ Crystal/Ceramic Resonator（外部晶振，8M）（如果这里选Disable则无法使用外部高速晶振）


    （图片仅供示意，忽略右边的芯片设置）
![img1](https://img-blog.csdnimg.cn/5a4b2bf01e6e4446a2ba9f5929691fce.png)

- （5）单击右边的PC13（因为板载LED灯接的PC13所以这里选PC13，可按照自己的要求自行设定） → GPIO_Output


    （图片仅供示意，右边的芯片设置同理）
![img1](https://img-blog.csdnimg.cn/1afbb093bc3141f9a82214a34b2fba0e.png)
![img1](https://img-blog.csdnimg.cn/10a29d9d5b6043da94542ee13ff65b8c.png)
- （6）设置好之后PC13变成绿色


- （7）单击Clock Configuration 

在这里输入72，按下回车 → OK，自动配置时钟频率为72Mhz
![Alt text](./imgs_1/image8.png)

- （8）单击Project Manager → Project ，配置准备要生成的工程
![img1](https://img-blog.csdnimg.cn/ea7d86e6c4a94d04a88338f1659691a0.png)

    注意：这里IDE这一栏请选择MakeFile（因为我们用VSCode + cmake编写和调试）
    
- （9）单击Code Generator 单选Copy only the nacassary library files，勾选Generate peripheral…peripheral，上述的配置都设置好后就可以单击右上角的GENERATE CODE生成工程了。
![img1](https://img-blog.csdnimg.cn/f8651dee15c84339aaafbcb4040d067b.png)

- ## VSCode配置

- 用VSCode打开刚刚创建工程的文件夹

- 先安装拓展：stm32-for-vscode

![Alt text](./imgs_1/image1.png)

- 依次打开工程结构树，双击main.c开始写源码

![Alt text](./imgs_1/image2.png)

- 找到Drivers文件夹里的stm32f1xx_hal_gpio.c打开，找到第465行的HAL_GPIO_WritrPin函数，复制其函数名，并在main方法里的while(1)调用
![Alt text](https://img-blog.csdnimg.cn/a532e18db16547a0a45cd5aee1349b05.png)

- 开始build

![Alt text](./imgs_1/image3.png)
![Alt text](./imgs_1/image4.png)

- 没有报错，开始flash上去
![Alt text](./imgs_1_1/image5.png)
![Alt text](./imgs_1_1/image6.png)

- 板载LED亮
![Alt text](./imgs_1_1/image7.png)

- ## 调试（待更新）