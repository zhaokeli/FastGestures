# FastGestures

- [FastGestures](#fastgestures)
  - [本软件目的](#本软件目的)
  - [特别注意](#特别注意)
  - [手势组合建议](#手势组合建议)
  - [热键](#热键)
  - [手势助记符](#手势助记符)
  - [鼠标手势](#鼠标手势)
  - [连续手势](#连续手势)
  - [精确式触控板手势](#精确式触控板手势)
  - [应用列表](#应用列表)
  - [配置项](#配置项)
    - [手势键](#手势键)
    - [手势超时时间](#手势超时时间)
    - [手势方向限制](#手势方向限制)
    - [鼠标下窗口](#鼠标下窗口)
    - [手势提示](#手势提示)
    - [全局手势键](#全局手势键)
    - [其它配置项](#其它配置项)
  - [执行的操作](#执行的操作)
    - [命令行](#命令行)
    - [打开/激活应用](#打开激活应用)
    - [快捷键](#快捷键)
    - [快捷键组](#快捷键组)
    - [窗口操作](#窗口操作)
    - [激活手势界面](#激活手势界面)
    - [Lua脚本](#lua脚本)
      - [可用内置函数](#可用内置函数)
        - [fg_active_main_winows()](#fg_active_main_winows)
        - [fg_show_msg(string)](#fg_show_msgstring)
        - [fg_send_shortcut_group(string)](#fg_send_shortcut_groupstring)
        - [fg_get_clipboard_text()](#fg_get_clipboard_text)
        - [fg_set_clipboard_text(string text)](#fg_set_clipboard_textstring-text)
        - [fg_set_windows_top(int hwnd)](#fg_set_windows_topint-hwnd)
        - [fg_sleep(int time)](#fg_sleepint-time)
        - [fg_get_mouse_windows_hwnd()](#fg_get_mouse_windows_hwnd)
        - [fg_get_mouse_windows_path()](#fg_get_mouse_windows_path)
        - [fg_parse_screen_qrcode()](#fg_parse_screen_qrcode)
        - [fg_active_application(string fullPath,int isRunAs)](#fg_active_applicationstring-fullpathint-isrunas)
        - [fg_send_text(string text)](#fg_send_textstring-text)
        - [fg_create_qrcode(string text)](#fg_create_qrcodestring-text)
        - [fg_volume_inc()](#fg_volume_inc)
        - [fg_volume_dec()](#fg_volume_dec)
        - [fg_volume_switch()](#fg_volume_switch)
        - [fg_brightness_inc()](#fg_brightness_inc)
        - [fg_brightness_dec()](#fg_brightness_dec)
        - [fg_run_cmd(string cmdStr,int isShow,int isReturn)](#fg_run_cmdstring-cmdstrint-isshowint-isreturn)
        - [fg_get_pid_by_name(string processName)](#fg_get_pid_by_namestring-processname)
        - [fg_mouse_wheel(int direction,int num,int times,int delay)](#fg_mouse_wheelint-directionint-numint-timesint-delay)
      - [fg_get_selected_files_path(int type)](#fg_get_selected_files_pathint-type)
        - [其它示例](#其它示例)
    - [扩展功能](#扩展功能)
  - [常见问题解决文案](#常见问题解决文案)
  - [问题反馈](#问题反馈)

![image](https://raw.githubusercontent.com/zhaokeli/FastGestures/3061c102560f81d42bdd325d9a16ef9171accfd1/fg.png)

## 本软件目的

使用鼠标或触控板定义一组组合的助记符，同时映射一个操作，执行一些软件功能，提高电脑使用效率，比如经常在各软件之前切换激活，打开系统便签，记事本，繁琐的右键复制，粘贴等等. 尽情发挥你的想象自定义自己常用的操作。

## 特别注意

1、此软件最好别跟其它手势软件一块打开混用，可能出现鼠标假死等情况，如果出现右键不能使用的情况可按下 ctrl+shift+alt+Q 强制退出  
2、手势方向限制模式会影响手势识别，速度模式：当画出多个方向时，斜方向会干扰识别率，所以软件采用一种速度算法，画的速度达到一个临界点，此时不会再识别出斜方向的手势，以提高手势识别率 ,一个明显的现象：当你速度很快的画 ```↗↙``` 这个手势时出来的可能是```↗←```，如果使用一般速度画才会识别为 ```↗↙```
3、鼠标手势以手势键弹起为结束然后执行对应操作和触控板手势以所有手指离开触控板为结束然后执行对应操作

## 手势组合建议

同一类操作先画一组方向手势，然后配合左中右键多次点击，组合成不同的手势组合，如：```→◐``` ```→◐◐``` ```→↑◐``` ```→↑◐◐```, 这样可减少手势记忆

## 热键

1、Ctrl+1 激活软件主界面  
2、Ctrl+Shift+Alt+Q  退出软件  

## 手势助记符

1、八个方向的基本手势 →  ↑ ← ↓ ↗ ↖ ↙ ↘  
2、◐ 鼠标左键  
3、◑ 鼠标右键  
4、◉ 鼠标中键  
5、◈ 鼠标X键  
6、▲ 鼠标滚轮向上一次  
7、▼ 鼠标滚轮向下一次  

## 鼠标手势

1、鼠标移入屏幕四角落，触发四个触发角事件
2、屏幕四个边缘宽50px 高为屏幕宽/高50%，3秒内连续划入3次，触发四个敲击边事件
3、鼠标画出的任意方向和按键组合  

## 连续手势

连续手势只支持鼠标,遇到鼠标滚轮滚动时可连续触发指定操作，当鼠标滚轮滚动时会出现一个滚动方向,在此手势之前可任意添加方向、点击手势等，遇到滚动方向手势时连续滚动会触发当前对应的操作，
如果关闭连续手势，则滚动时会出现多个滚动方向手势(默认为此)

## 精确式触控板手势

手指放到触控板上即为手势开始，除了默认忽略的几个操作外均可画出手势符号。  

1、四个角落、四个边、单击事件  
2、2，3，4，5指，在触控板上短按、长按事件，时间可自定义  
3、忽略单指，两指系统默认操作行为，(两指可一指按下，另一指画手势 用法参考Betterandbetter：[查看单指画手势视频](https://13315641.s21v.faiusr.com/58/1/ABUIABA6GAAgmtnK_AUoxN37-gI.mp4>)  
4、三指拖动启用后，三指画手势符号会被忽略  

5、三指：先放上去，左中右单击并抬起后分别代表 鼠标左中右单击手势，同时可画方向手势,也可定义三指为左键或中键拖动功能  
6、其它情况可使用几个手指同时画出指定手势  

## 应用列表

列表中每一个应用后面有继承和排除两项设置，继承：除了使用本应用里设置的手势外也可以使用全局中设置的手势，排除：勾选后在此应用中不使用任何手势  
>全局项设置，全局里只有一个排除项设置，勾选后手势只会作用于添加到应用列表中的应用, 没有添加的应用不会显示手势轨迹

## 配置项

### 手势键

为了方便配合触控板上单指画手势的操作，添加了自定义手势键功能，按下键盘上自定义的手势键后，单指和鼠标可直接画手势

手势键：中 右 X键 自定义键 任意一个按下，移动大于4个像素后开始识别手势轨迹方向键，除了方向键，也可按下鼠标其它非触发手势的按键来插入手势符号形成组合(无需移动鼠标)
最终手势可由上面7种助记符随机组合完成

### 手势超时时间

手势超时时间,<=3000不限,>=3000时，超过设置的时间手势还没有结束，则取消本次手势识别

### 手势方向限制

1、不限制，画方向时不限制识别的方向，由软件自行优化，画手势速度很快的时候，不再识别出斜方向手势，首个方向没有此限制  
2、正方向，只识别正方向的四个方向键，首个方向没有此限制  
3、斜方向，只识别斜方向的四个方向键，首个方向没有此限制  

### 鼠标下窗口

当执行快捷键和窗口操作时，此项若开启则会激活当前鼠标下窗口，并作用于此窗口，若关闭则会作用于当前激活的窗口

### 手势提示

开启后，会在屏幕左下角提前显示当前可用的手势项

### 全局手势键

设置此手势键后，用此手势键画出的手势全为全局手势

### 其它配置项

其它配置项，见名其意，应该很好理解，不再多解释

## 执行的操作

### 命令行

可调用系统命令来执行对应的操作

### 打开/激活应用

 查找应用的主窗口，如果不存在则启动它

### 快捷键

录入想要执行的快捷键

### 快捷键组

此种操作可一次分开执行多个快捷键。  

如：复制一个地址后希望在谷歌浏览器中画一个手势完成地址栏获得焦点，粘贴地址，回车访问这个连续的操作, 需要执行的按键依次为：ctrl+L 选择地址栏, ctrl+v 粘贴地址，enter访问地址。  
可设置如下json结构，其中delay为每个快捷键操作之前的延时时间，单位毫秒,vk_code 接收十六进制虚拟码。具体的键码可在此处获得, [查看全部虚拟键码](https://docs.microsoft.com/en-us/windows/win32/inputdev/virtual-key-codes)

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

### 窗口操作

可作用于当前鼠标下窗口，执行对应的操作

### 激活手势界面

打开手势软件的主界面

### Lua脚本

可输入自己的lua脚本，内容可以为下面几种形式  
1、直接输入lua脚本内容  
2、单行输入脚本文件所在的绝对路径  
3、放入预置的脚本目录,位置二选一
  C:\Program Files\FastGestures\LuaScript
  C:\Users\xxxx\AppData\Roaming\zhaokeli.com\FastGestures\LuaScript

当脚本为文件时可使用以下预置全局变量

* __FILE__ 脚本全路径
* __DIR__  脚本所在路径,结尾不带斜线

#### 可用内置函数

##### fg_active_main_winows()

激活手势主窗口

##### fg_show_msg(string)

显示一个消息提示

```lua
fg_show_msg("一个提示消息");
```

##### fg_send_shortcut_group(string)

发送一组快捷键，参数为json字符串,同上面快捷键组一样

```lua
local keyList=[[
[
  {
    "delay": 10,
    "buttons": [
      {
        "vk_code": "0xA2",
        "vk_name": "Ctrl"
      },
      {
        "vk_code": "0x12",
        "vk_name": "Alt"
      },
      {
        "vk_code": "0x4C",
        "vk_name": "L"
      }
    ]
  },
  {
    "delay": 100,
    "buttons": [
      {
        "vk_code": "0xA2",
        "vk_name": "Ctrl"
      },
      {
        "vk_code": "0x53",
        "vk_name": "S"
      }
    ]
  }
]
]]
fg_send_shortcut_group(keyList);
```

##### fg_get_clipboard_text()

获取当前剪切板文本内容

##### fg_set_clipboard_text(string text)

设置剪切板文本

##### fg_set_windows_top(int hwnd)

设置窗口置顶或取消,参数传0时,默认为当前鼠标下的窗口

##### fg_sleep(int time)

挂起/延时时间，单位毫秒

##### fg_get_mouse_windows_hwnd()

取当前鼠标下的窗口句柄

##### fg_get_mouse_windows_path()

取当前鼠标下的窗口可执行文件路径

##### fg_parse_screen_qrcode()

从屏幕上解析出二维码内容，如果不存在二维码则返回空字符串

##### fg_active_application(string fullPath,int isRunAs)

打开或激活应用，fullPath应用的全路径，isRunAs是否使用管理员权限执行

##### fg_send_text(string text)

发送文本

##### fg_create_qrcode(string text)

生成并显示一个二维码

##### fg_volume_inc()

音量加

##### fg_volume_dec()

音量减

##### fg_volume_switch()

静音/关闭静音切换

##### fg_brightness_inc()

屏幕亮度加,（部分屏幕不支持）

##### fg_brightness_dec()

屏幕亮度减，（部分屏幕不支持）

##### fg_run_cmd(string cmdStr,int isShow,int isReturn)

执行命令行并取返回值,cmdStr命令，isShow是否显示命令行窗口，isReturn是否取返回值，特别注意取返回值时确保调用的程序会自动退出。

##### fg_get_pid_by_name(string processName)

通过进程名字取Pid,多个相同名字进程只取首个，名字忽略大小写

##### fg_mouse_wheel(int direction,int num,int times,int delay)

鼠标滚轮事件
direction 0:向下滚动 1:向上滚动
num 每次滚动距离
times 滚动次数
delay 多次滚动时延时默认10毫秒

#### fg_get_selected_files_path(int type)

type 0:返回选中所有的(文件/目录)路径，1:返回选中文件路径,2:返回选中目录路径

返回结构为一个元表，示例,取选中的第一个文件路径

```lua
local fileList=fg_get_selected_files_path(1);
fg_show_msg(fileList[0]);
```

##### 其它示例

```lua
-- 设置文本
fg_set_clipboard_text("Lua 变量");
-- 暂停1秒
fg_sleep(1000);
-- 取文本
local tex=fg_get_clipboard_text();
--提示信息
fg_show_msg(tex);
```

### 扩展功能

更多扩展可加QQ群下载  

一个扩展至少有两个文件 ``plugin.json`` 配置文件，一个主执行文件 ``main.lua``,主执行文件由配置文件中来指定  
一个扩展一个目录，目录名字可随意，但``plugin.json``中``uuid``字段必须唯一，且以后也不能变更  
扩展目录可放于软件安装目录``C:\Program Files\FastGestures\Plugins``，或用户数据目录``C:\Users\xxxx\AppData\Roaming\zhaokeli.com\FastGestures\Plugins``  

可使用软件扩展管理->新建扩展来初始化一个新扩展目录
  
``plugin.json``结构如下

```json
{
 "uuid":"17963bd79d6b170eace6e1a489332363",
 "name":"搜索客户表",
 "version":"1.0.0",
 "desc":"搜索客户表",
 "executeFileName":"main.lua",
 "type":0,
 "author":"zhaokeli",
 "iconPath":"icon.png"
}
```

+ ``uuid``: 32位唯一标识,不符合规则会忽略
+ ``name``: 扩展名字
+ ``version``: 扩展版本
+ ``desc``: 扩展描述
+ ``executeFileName``: 可执行文件名,相对Plugins目录的路径，如果在目录里请带上路径,开头不带斜杠
+ ``type``: 可执行文件类型，0：lua脚本，1：windows可执行程序
+ ``author``: 扩展作者
+ ``iconPath``: 扩展图标，可空，同样是相对路径开头不带斜杠

下面是一个脚本，实现``Ctrl+F`` 、 ``Ctrl+A`` 、``发送文件`` 、的一连串功能  ，文本从命令行入参``arg[1]``取得
``main.lua``

```lua
local keyList=[[
[
  {
    "delay": 10,
    "buttons": [
      {
        "vk_code": "0xA2",
        "vk_name": "Ctrl"
      },
      {
        "vk_code": "0x46",
        "vk_name": "F"
      }
    ]
  },
  {
    "delay": 100,
    "buttons": [
      {
        "vk_code": "0xA2",
        "vk_name": "Ctrl"
      },
      {
        "vk_code": "0x41",
        "vk_name": "A"
      }
    ]
  }
]
]]
fg_send_shortcut_group(keyList);
fg_send_text(arg[1]);

```

选择扩展功能后，根据扩展的使用方法，是否需要设置命令行入参来执行对应的功能，执行操作时可传入命令行参数，脚本或可执行文件可解析此参数来执行对应的操作  

lua脚本中取命令行中的参数有两种

* 直接使用arg[0]，arg[1]，来取以空格分隔的命令参数
* 使用全局变量cmd_params[name]，取对应的值，例 --name="keli zhao" --path=E:/test

lua脚本中依然可用预置的全局变量

## 常见问题解决文案

1、如果出现在一些窗口(任务管理器等)上手势失效，请到安装目录或开始菜单安装证书到受信任的根证书目录. 证书为本人博客域名实名认证,请放心安装！  
2、电脑上安装有360卫士杀毒的用户,请加将本软件加入信任,并关闭驱动防护.因为360卫士和杀毒视所有模拟鼠标、键盘操作的非付费认证签名软件均为恶意软件,会直接驱动拦截,本软件用到鼠标(画轨迹)，键盘(发送快捷键)，此操作会导致右键失效.加信任和关防护后还不能使用的,可以尝试退出/卸载360后再次尝试使用，Win10自带安全软件也是不错的选择哟!  
3、如果遇到拖动文件到一些编辑等软件上出现不可用的情况，请重启手势软件和编辑器后再次尝试，当前以普通用户登陆，而手势软件和编辑器使用管理员权限打开的情况下会遇到此种问题。  
4、打开/激活应用功能，如果遇到一开始可以正常激活，后来又激活不了了，可尝试重启软件来解决  
5、如果安装成功，启动时出现0xC000007b错误，可能因为系统运行库损坏，请重新下载vc运行库修复 <https://www.microsoft.com/zh-CN/download/details.aspx?id=48145>

6、如果win7下出现部分emoji字符不显示，可下载 ```Segoe UI Emoji``` (600K)字体安装后重启软件

7、如果出现启动异常或崩溃，请修复系统相关运行库文件，
打开微软官网 <https://docs.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170>，
64位运行库 <https://aka.ms/vs/17/release/vc_redist.x64.exe>
32位运行库 <https://aka.ms/vs/17/release/vc_redist.x86.exe>

## 问题反馈

QQ群:  [89193444](https://jq.qq.com/?_wv=1027&k=mOqSBLo7)  
QQ: 735579768  
微信: kelicom  
