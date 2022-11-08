## 使用 CLion 调试树莓派Pico

> 使用树莓派（如Raspberry Pi 4B）直接调试 Pico 是可行的，因为树莓派有 SWD 接口。对于本地开发来说可以使用官方提供的 [Picoprobe](https://github.com/raspberrypi/picoprobe) 项目结合 CLion 实现嵌入式代码调试。

### 环境配置

官方文档在 [Appendix A: Using Picoprobe](https://datasheets.raspberrypi.com/pico/getting-started-with-pico.pdf) 一节详细讲述了 `Picoprobe` 的操作步骤。其中连线为：

![截屏2022-10-18 11.06.03](https://ink-note.oss-cn-chengdu.aliyuncs.com/images/2022/11/07/1667832585108-KTVkQw.png)

> UART连线可以不连接，并不影响调试，只是可以用来转发UART消息到本机

### 配置 CLion 调试

> 电脑系统为 macOS

打开「编辑配置」> 添加一个「嵌入式GDB服务器」

+ GDB 默认`Bundled GDB`
+ target remote ：`tcp:localhost:3333`
+ GDB 服务器选择上一节配置过的 `src/openocd` 的路径
+ GDB 参数为：`-f interface/picoprobe.cfg -f target/rp2040.cfg -s tcl`
+ 注意需要添加工作目录，不然无法找到`picoprobe.cfg`和`rp2040.cfg`，路径为上一节`openocd`的安装路径

![截屏2022-10-18 11.11.48](https://ink-note.oss-cn-chengdu.aliyuncs.com/images/2022/11/07/1667832500073-ZiV7oY.png)

还有就是「外设」中加载`.svd`文件路径为`$PICO_SDK_PATH/src/rp2040/hardware_regs/rp2040.svd`

### 参考

[Want to Flash and Debug an MCU Over the Air? Just Use Your Raspberry Pi](https://blog.jetbrains.com/clion/2021/03/flash-debug-over-air)

[使用picoprobe调试树莓派PICO（附调试包）](https://zhuanlan.zhihu.com/p/524649549)

[RaspberryPi Pico Dev Board](https://timsavage.github.io/rpi-pico-devboard/)