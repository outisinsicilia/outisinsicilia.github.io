
### 免PE系统内置重装方法

> 设置-系统-恢复-重置此电脑（初始化电脑）
 
- 如果事先做好了硬盘分区，就算选择抹除所有数据，实际上也只会抹除C盘。
- 重置过程如果卡进度条，可以试试关代理断网。

### 重装后新手向导跳过联网

- shift+F10，打开命令提示符，输入OOBE\BYPASSNRO后回车，系统自动重启后联网界面出现“我没有Internet链接”。

### 删除桌面“了解此图片相关信息”图标（保留Windows聚焦壁纸）

- win+R打开“运行”，输入regedit（或直接用搜索框输入），打开注册表编辑器，找到路径：

> HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Explorer\HideDesktopIcons\NewStartPanel

- 在NewStartPanel文件夹内新建一个DWORD (32 位)值，命名为：

> {2cc5ca98-6485-489a-920e-b3e88a6ccce3}

- 数据数值修改为1，保存。

### 添加小鹤双拼双拼方案

- 注册表编辑器找到：

> HKEY_CURRENT_USER\Software\Microsoft\InputMethod\Settings\CHS

- 新建一个字符串值，命名为UserDefinedDoublePinyinScheme0，数值数据为：

> 小鹤双拼*2*^*iuvdjhcwfg^xmlnpbksqszxkrltvyovt

### 完全卸载Edge浏览器

- 先下好别的浏览器。
- 移除工具见：https://github.com/ShadowWhisperer/Remove-MS-Edge/
- 按需移除，我是只移除Edge（Edge Only）

### 彻底移除windows defender

- 无特殊需求的话，下个安全软件接替WD的工作即可。
- 操作流程见：https://www.bilibili.com/video/BV1TTcBe2E9t/
- 事先在windows安全中心关闭“篡改防护”，然后开始修改（实测重启后部分注册表会复原，可以再改一遍）
- 注册表编辑器找到：

> HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender

- 所有要改的项目（方便复制粘贴，皆为新建一个DWORD (32 位)值，并把数值改为1）

原有项：
Windows Defender：
```
DisableAntiSpyware
DisableRealtimeMonitoring
DisableAntiVirus
DisableSpecialRunningModes
DisableRoutinelyTakingAction
ServiceKeepAlive
```

新建项（在windows defender目录下新建）：

Real-Time Protection：
```
DisableBehaviorMonitoring
DisableOnAccessProtection
DisableRealtimeMonitoring
DisableScanOnRealtimeEnable
```

Signature Updates：
`ForceUpdateFromMU`

Spynet：
`DisableBlockAtFirstSeen`

### 修改保存、缓存路径（避免占用c盘）

- 各个软件的设置里。
- 浏览器下载、图片、视频、文档等默认文件夹：

> 右键-属性-位置-移动…

~回收站：~

~右键-属性-回收站位置选c盘-选择“不将文件移动到回收站中”~

> [!CAUTION]
> 上述方法无法改变回收站路径，并且还会导致所有属于C盘的文件直接删除而不进入回收站。

### 无会员去除spotify的win端广告

- 破解见：https://github.com/SpotX-Official/SpotX?tab=readme-ov-file/
- 在这个网站下载1.2.68或其以前版本的spotify：https://loadspot.pages.dev/
- 注意其必定会被WD报毒，导致下载后会被直接删除。先移除WD。

### 任意程序自定义开机自启

- 将原文件或快捷方式放入：

> C:\Users\（你的用户名）\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup

- 快速找到该文件夹的方法：win+R打开“运行”，输入shell:startup，即可直接打开该文件夹。

### 删除大文件hiberfil.sys（即关闭windows休眠模式）

- 以管理员模式运行命令提示符或powershell，输入以下命令并回车：

> powercfg -hibernate off