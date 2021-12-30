## 移动机器人位姿调整算法

### <span id="ch0">文档说明</span>  

**1-环境**
- Ubuntu16.04 
- ros-kinetic 

**2-参数声明**

- 坐标系声明：以机器人中心为原点，机器人正方向为z轴，向右为x轴

- 深度相机获取二维码的相对机器人的位姿包括三维位置坐标x,y,z，和三维角度坐标r,p,y
- 其他参数请参考[逻辑图](https://www.wolai.com/6SWGBHGcL499XUCnz1mqT5)

>注：1.假设二维码贴于墙面，则垂直于墙面方向为二维码正方向

>   2.本程序只使用x，z，p（机器人正方向与二维码正方向之间的夹角）来对机器人位姿进行调整

**3-代码逻辑**
> 输入：req.x，req.z，req.type

type|function
---|---
0|调整z，z<req.z则后退
1|调整角度，使得机器人中心正对二维码
2|移动到二维码正前方req.z位置
3|调整角度，与二维码正方向平行即p=0
4|运行整个程序，依次运行type=0，1，2，3，5，3
5|调整x，使得机器人停在req.x位置

- [逻辑图](https://www.wolai.com/6SWGBHGcL499XUCnz1mqT5)（逻辑图参考）

**4-调用接口**

ros命令行
- rosservice call /tuning_pose type="4" x="0" z="0.42"
