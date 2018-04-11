# 安装sogou输入法

安装搜狗输入发首先需要安装fcitx

1. 添加fcitx键盘输入法系统
`sudo add-apt-repository ppa:fcitx-team/nightly`

2. 更新系统
`sudo apt-get update`

3. 安装fcitx
`sudo apt-get install fcitx`

4. 安装fcitx配置工具
`sudo apt-get install fcitx-config-gtk`

5. 安装fcitx的table-all软件包
`sudo apt-get install fcitx-table-all`

6. 安装im-switch切换工具
`sudo apt-get install im-switch`

7. 到搜狗官网下载linux版输入法，默认文件保存在Downloads目录下。进入此目录执行
`sudo dpkg -i 输入法文件名.deb`

8. 设置语言选项
点击界面右上角齿轮，选择系统设置->语言支持,可能会提示你需要执行`sudo apt-get install -f`命令。
如果没有提示，则将弹框中最下面的输入法系统改为**fcitx**。

9. 重启系统

10. 点击右上角键盘图标，选择下拉菜单中的设置选项或直接在终端中执行`fcitx-config-gtk3`。弹出设置窗口，
点击弹出窗口最下面的**+**，取消勾选**Only Show Current Language**后，搜索搜狗拼音，选中后确定。