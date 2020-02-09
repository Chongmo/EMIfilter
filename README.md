# EMIfilter
Simulink program for graduate design
## 20200208工作计划

计划建立输出电流的频域模型，初步计划使用示波器输出的波形数据做fft变换。因为之前有试过在simulink模型里加FFT模块，但是它看起来是每一次采样时间都做了傅里叶变换，最终得到的波形只是仿真停止的时刻的频域波形…今天找一找原因。

## 工作内容

今日工作内容：给现在的逆变器按正常的方法加一个滤波器

![img](http://github.com/Chongmo/EMIfilter/blob/master/images/clip_image002.png)

该图为傅里叶变换后的输出电流频域图像。

![img](file:///C:/Users/DELL/AppData/Local/Temp/msohtmlclip1/01/clip_image004.png)

为选择合适的滤波器，将其纵坐标转化为以dB为单位的图像，可知我们要使150Hz的谐波过滤掉，低通滤波器在该频率应当衰减23dB左右。

![img](file:///C:/Users/DELL/AppData/Local/Temp/msohtmlclip1/01/clip_image006.jpg)

将目标滤波进行归一化操作，以确定滤波器的阶数。我暂时选择了切比雪夫滤波器。

![img](file:///C:/Users/DELL/AppData/Local/Temp/msohtmlclip1/01/clip_image008.jpg)

通带纹波为3dB时，二阶的滤波器即可满足要求。

![img](file:///C:/Users/DELL/AppData/Local/Temp/msohtmlclip1/01/clip_image010.png)

原电流为i，我放的切比雪夫滤波器为蓝线，红线是默认状态下的低通滤波器。可以看到在阶数增加以及通带纹波增加的情况下波形的幅值会有一定衰减，但如果阶数过低的话，滤波效果可能会减弱。

今日工作代码：https://github.com/Chongmo/EMIfilter/tree/Chongmo-20200208

## 第二天计划

通过和学长的交流我觉得我对电磁干扰的原理的理解还是不太透彻，所以接下来的几天里我还是会再多看一下关于EMI的论文，确定一下电磁干扰滤波和普通滤波的区别。

以及不确定MATLAB仿真时是直接使用IGBT/Diode组合就可以了，还是需要再详细一点把IGBT的内部结构都仿真出来。按照现在的仿真结果，电磁干扰造成的波动要远远小于它本来的纹波？我觉得我还需要再了解一下抑制共模干扰、差模干扰的原理，再检查一下现有的仿真模型。

明日预计工作时间：3h
