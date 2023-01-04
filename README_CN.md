HUIS UI CREATOR（工程预览）
====

HUIS UI CREATOR 是用于创建 HUIS 远程控制 UI 的 PC 应用程序。

## 解释

HUIS UI CREATOR可以从多个设备的按键中挑选出您常用功能的按键，打造您最喜欢的HUIS遥控器UI。 您可以更改按钮的位置和大小，以及更改标签和图像。

## 如何使用

#### 谨慎

此存储库不分发应用程序二进制文件。 确认后述“如何构建”后，需要构建并打包此仓库的源码。

此外，使用 HUIS UI CREATOR 时，需要将 HUIS 主机连接到 PC。

#### 更新文件

要反映使用 HUIS UI CREATOR 创建的遥控器，需要更新 HUIS。
请参考[这里（如何更新HUIS REMOTE CONTROLLER）](firmware/readme.md)。

如需使用HUIS UI CREATOR，请将HUIS远程控制软件更新至4.1.0或以上版本。

====

#### 开始申请
1. 将 HUIS 连接到您的电脑。
2. 启动 HUIS UI CREATOR。 开机时，HUIS主机的遥控信息会与PC同步。 同步可能需要一分钟或更长时间才能完成。
3. 同步完成后，回到主界面。 遥控器列表显示在主屏幕上。

#### 创建一个新的遥控器
1. 在主屏幕显示的遥控器列表中，点击左侧标有“+”的遥控器。
2. 转换到遥控器编辑屏幕。

###### 遥控器编辑画面说明
- 遥控编辑画面右半部分的遥控部分称为“调色板遥控”，左半部分的遥控部分称为“画布遥控”。 通过将按钮放在画布遥控器上的调色板遥控器上来创建遥控器。
- 从调色板遥控器上方的列表中选择一个设备以切换调色板遥控器的内容。
- 如果拖放或双击放置在调色板遥控器上的按钮，该按钮将放置在画布遥控器上。
- 从调色板遥控器上方的列表中选择“常用”，以查看填充有标签和图像等项目的遥控器。 双击标签或图像项目会将项目放置在画布遥控器上。
- 如果您选择放置在画布上的项目，您可以用鼠标改变它的位置。 您可以通过操作所选项目四个角上显示的方块来更改项目的大小。
- 当您点击放置在画布上的项目时，该项目的属性编辑框将出现在画布遥控器的左侧。
- 您可以通过单击画布上未放置项目的部分来在属性编辑框中设置背景图像。
- 点击画布遥控器上的【新建页面】，为遥控器添加页面。 一个遥控器的最大页数为 5。
- 您可以在画布遥控器顶部的文本框中设置遥控器名称。 必须设置遥控器的名称。

###### 保存遥控器
1. 按下遥控器编辑画面左上角的[完成]按钮。
2. 选择【保存并返回首页】将编辑的内容反映到HUIS主机。 这时需要将HUIS主机连接到PC。
3. 保存后，返回主屏幕。

#### 编辑现有的遥控器
1. 从主屏幕显示的遥控器列表中单击要编辑的遥控器。
2. 转换到遥控器编辑屏幕。

遥控器编辑屏幕与创建新遥控器时相同。

#### 删除创建的远程
1. 在主屏幕的遥控器列表中右键单击要删除的遥控器，在右键菜单中选择“删除遥控器”。

#### 退出应用程序
您可以通过按应用程序的关闭按钮来终止应用程序。 此时正在编辑的遥控器会丢失，所以退出前一定要和HUIS同步。

#### 使用创建的遥控器

1.同步PC和HUIS后，断开PC和HUIS。 当 HUIS 与 PC 断开连接时，HUIS 将自行处理编辑内容的反映。 在此过程中，HUIS将暂时停止接受操作。
2. 当您可以再次操作HUIS 主机时，请检查用HUIS UI CREATOR 创建的遥控器是否已添加到HOME 屏幕的遥控器列表中。 如果未添加创建的遥控器，请在转换到另一个屏幕后再次显示 HOME 屏幕。



## 如何构建

描述构建和使用此存储库源代码的过程。

#### 准备

搭建前，准备如下开发环境。

| Requirement                                                                 | Remarks                                       |
|:----------------------------------------------------------------------------|:----------------------------------------------|
| [Python 2.6 or 2.7](https://www.python.org/downloads/)                      |                                               |
| [Ruby](http://rubyinstaller.org/)                                           |                                               |
| [Node.js](http://nodejs.org/download/ )                                     |                                               |
| [Compass](http://compass-style.org/)                                        |                                               |
| [Grunt CLI](https://github.com/gruntjs/grunt-cli)                           |                                               |
| [compiler for node-gyp](https://github.com/TooTallNate/node-gyp/)           | Required for compiling native Node.js modules |
| [electron-packager](https://github.com/electron-userland/electron-packager) |                                               |

#### 构建说明

1.获取源代码。

         $ git clone https://github.com/sony/huis-ui-creator.git

2. 转到克隆的目录。

         $ cd huis-ui-creator

3. 执行以下命令。

         $ npm 安装

4. 使用以下命令构建本机模块。 （对于 Windows 32 位，Mac 不需要）

        $ cd node_modules
        $ cd usb_dev
        $ set HOME=~/.electron-gyp
        $ node-gyp rebuild --target=1.4.10 --arch=ia32 --dist-url=https://atom.io/download/atom-shell
        
   请相应地更改 Electron 版本 `--target`。 此外，如果您为 Windows 64 位构建，请更改为“--arch=x64”。

5. 再次进入`huis-ui-creator`的根目录。

6. 使用以下命令构建 TypeScript 和 SCSS。

        $ grunt build

对于 Mac，添加“--platform=darwin”，如下所示。

        $ grunt build --platform=darwin

7. grunt构建完成后，会在`www/app`下输出编译好的TypeScript和SCSS。 将以下文件和目录复制到 Electron 打包的 www 目录中。

   -package.json
   -main.js
   -node_modules 目录

   复制 `node_modules` 目录时忽略任何“路径太长”错误或警告。

#### 包装
如上所述使用grunt构建后复制文件后，您可以通过执行以下命令对其进行打包。 （对于 Windows 32 位）

    $ cd <huis-ui-creator dir>\www
    $ electron-packager . <app name> --platform=win32 --arch=ia32 --electron-version=1.4.10 --ignore="node_modules/(grunt*|electron-rebuild)" --ignore=".git" --ignore="Service References" --ignore="docs" --ignore="obj" --ignore="tests/*" --ignore="www" --ignore="platforms" --ignore="-x64$" --ignore="-ia32$"

选请相应地更改 Electron 版本 `--target`。 此外，如果您为 Windows 64 位构建，请更改为“--arch=x64”。 但是，请指定与构建上述本机模块时相同的 `--target` 和 `--arch` 选项。
为 Mac 64 位构建时，请更改为 `--platform=darwin`、`--arch=x64`。

`<app name>` 用于打包后的文件存放目录，可执行文件名等。 请指定任何应用名称。

打包完成后，会在`<app name>-win32-ia32`目录下生成包（Windows 32位，Mac 64位`<app name>-darwin-x64`）。

启动 `<app name>.exe`（对于 Mac 为 `<app name>.app`）并确认它可以工作。

##免责声明
本源代码用于开发，产品版本在设计等方面存在差异。


## 执照

版权所有 2016 索尼公司

根据 Apache 许可证 2.0 版（“许可证”）获得许可；除非遵守许可证，否则您不得使用此文件。

http://www.apache.org/licenses/LICENSE-2.0

除非适用法律要求或书面同意，否则根据许可分发的软件是在“按原样”的基础上分发的，没有任何形式的保证或条件，无论是明示的还是暗示的。
