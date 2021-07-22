# FastGestures

![image](https://github.com/zhaokeli/FastGestures/blob/main/fg.png)

本软件目的: 快捷操作一些软件功能，能一只手完成的绝不用两只手，提高电脑使用效率

## 特别注意 
1、此软件最好别跟其它手势软件一块打开混用，可能出现鼠标假死等情况，如果出现右键不能使用的情况可按下 ctrl+shift+alt+Q 强制退出

## 常见问题解决文案:
1、如果出现在一些窗口(任务管理器等)上手势失效，请到安装目录或开始菜单安装证书到受信任的根证书目录. 证书为本人博客域名实名认证,请放心安装！  
2、电脑上安装有360卫士杀毒的用户,请加将本软件加入信任,并关闭驱动防护.因为360卫士和杀毒视所有模拟鼠标、键盘操作的非自家或大厂软件均为恶意病毒软件,会直接驱动拦截,本软件用到鼠标(画轨迹)，键盘(发送快捷键)，此操作会导致右键失效.加信任和关防护后还不能使用的,可以尝试退出/卸载360后再次尝试使用，win10自带安全软件也是不错的选择! 
3、如果遇到拖动文件到一些编辑等软件上出现不可用的情况，请重启手势软件和编辑器后再次尝试，当前以普通用户登陆，而手势软件和编辑器使用管理员权限打开的情况下会遇到此种问题

## 快捷键
1、Ctrl+1 激活软件主界面  
2、Ctrl+Shift+Alt+Q  退出软件  

## 屏幕预置手势

1、鼠标移入屏幕四角落，触发四个触发角事件  
2、屏幕四个边缘宽50px 高为屏幕宽/高50%，3秒内连续划入3次，触发四个敲击边事件  

## 精确式触控板

1、四个角落单指短按事件，时间可自定义  
2、2，3，4，5指，在触控板上短按、长按事件，时间可自定义  

## 自定义手势

鼠标操作助记符：

1、八个方向的基本手势 →  ↑ ← ↓ ↗ ↖ ↙ ↘  
2、◐ 鼠标左键  
3、◑ 鼠标右键  
4、◉ 鼠标中键  
5、◈ 鼠标X键  
6、▲ 鼠标滚轮向上一次  
7、▼ 鼠标滚轮向下一次  

触发开始记录手势的按键：中 右 X键 win键 任意一个按下，移动大于4个像素后开始识别手势轨迹方向键，除了方向键，也可按下鼠标其它非触发手势的按键来插入手势符号形成组合(无需移动鼠标)
最终手势可由上面7种助记符随机组合完成

## 触控板操作

手指放到触控板上即为手势开始，除了默认忽略的几个操作外均可画出手势符号。

1、忽略单指，两指系统默认操作行为，(两指可一指按下，另一指画手势 用法参考Betterandbetter：https://13315641.s21v.faiusr.com/58/1/ABUIABA6GAAgmtnK_AUoxN37-gI.mp4)  
2、三指拖动启用后，三指画手势符号会被忽略  

3、三指：先放上去，左中右单击并抬起后分别代表 鼠标左中右单击手势，同时可画方向手势,也可定义三指为左键或中键拖动功能
4、其它情况可使用几个手指同时画出指定手势  

## 执行的操作

### 命令行

可调用系统命令来执行对应的操作

### 打开/激活应用

 查找应用的主窗口，如果不存在则启动它

## 快捷键

录入想要执行的快捷键

## 快捷键组

此种操作可一次分开执行多个快捷键。  

如：复制一个地址后希望在谷歌浏览器中画一个手势完成地址栏获得焦点，粘贴地址，回车访问这个连续的操作, 需要执行的按键依次为：ctrl+L 选择地址栏, ctrl+v 粘贴地址，enter访问地址。  
可设置如下json结构，其中delay为每个快捷键操作之前的延时时间，单位毫秒,vk_code 接收十六进制虚拟码。具体的键码可在此处获得
<https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes>

```json
[
  {
    "delay": 500,
    "buttons": [
      {
        "vk_code": "0xA2",
        "vk_name": "Ctrl"
      },
      {
        "vk_code": "0x4C",
        "vk_name": "L"
      }
    ]
  },
  {
    "delay": 500,
    "buttons": [
      {
        "vk_code": "0xA2",
        "vk_name": "Ctrl"
      },
      {
        "vk_code": "0x56",
        "vk_name": "V"
      }
    ]
  },
  {
    "delay": 500,
    "buttons": [
      {
        "vk_code": "0x0D",
        "vk_name": "Enter"
      }
    ]
  }
]
```

## 窗口操作

可作用于当前鼠标下窗口，执行对应的操作

## 激活手势界面

打开手势软件的主界面

## Lua脚本

可输入自己的lua脚本，内容可以为下面几种形式
1、执行的脚本内容  
2、脚本文件所在的绝对路径  
3、脚本文件相对路径,在C:\Program Files\FastGestures\LuaScript目录中，或C:\Users\xxxx\AppData\Roaming\zhaokeli.com\FastGestures\LuaScript目录中
