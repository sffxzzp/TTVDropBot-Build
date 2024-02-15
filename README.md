# TTVDropBot-Build

## About this build

Currently using [PockySweet/Enhanced-TTVDropBot](https://github.com/PockySweet/Enhanced-TTVDropBot).

## Docker build

[Docker Repo](https://ghcr.io/sffxzzp/ttvdropbot-build)

Only `linux-x64` and `linux-arm64`, and I think it is enough for most use cases.

## EN

[TTVDropBot](https://github.com/PockySweet/Enhanced-TTVDropBot) builds of other architectures and systems.

Now supports:

* linux-x64
* linux-arm64
* win-x64
* win-arm64
* macos-x64
* macos-arm64

The binary files you may want to download is in [Here](https://nightly.kanojo.pp.ua/TTVDropBot-Build).

## CN

[TTVDropBot](https://github.com/PockySweet/Enhanced-TTVDropBot) 在各系统和架构下的构建。

现支持：

* linux-x64
* linux-arm64
* win-x64
* win-arm64
* macos-x64
* macos-arm64

构建好的二进制文件在 [这里](https://nightly.kanojo.pp.ua/TTVDropBot-Build) 下载。

### 小提示

使用反代（即 302 原理的同类应用及用法）访问 Twitch 的用户，需要临时给环境变量增加 `NODE_TLS_REJECT_UNAUTHORIZED=0` 以忽略证书错误。

简单一点，Win 下需要建立批处理，并使用批处理启动：

``` batch
@echo off
set NODE_TLS_REJECT_UNAUTHORIZED=0
ttvdropbot-v2.exe
```

自动重启版

``` batch
@echo off
:start
set NODE_TLS_REJECT_UNAUTHORIZED=0
set ttvdropbot_displayless=true
set ttvdropbot_games="Warframe Tom_Clancy's_Rainbow_Six_Siege Don't_Starve_Together Humankind Roller_Champions PAYDAY_2 The_Elder_Scrolls_Online Gwent:_The_Witcher_Card_Game The_Cycle:_Frontier"
set ttvdropbot_autoclaim=true
ttvdropbot-v2.exe
timeout /t 10
goto start
```

Linux 及 MacOS 下可以建立 .sh 脚本，并使用 sh 启动（可能需要先 `chmod +x ttvdropbot-v2` 增加执行权限）：

``` shell
export NODE_TLS_REJECT_UNAUTHORIZED=0
./ttvdropbot-v2
```

带判断的用法，可以切换 displayless 模式，带自动重启

``` shell
#/bin/bash
while true;
do
    count=`ps -e | grep "ttvdropbot" | grep -v grep | wc -l`
    if [ $? -eq 0 ]; then
        export NODE_TLS_REJECT_UNAUTHORIZED=0
        if [ $1 ]; then
            export ttvdropbot_displayless=true
            export ttvdropbot_games="Warframe Tom_Clancy's_Rainbow_Six_Siege Don't_Starve_Together Humankind Roller_Champions PAYDAY_2 The_Elder_Scrolls_Online Gwent:_The_Witcher_Card_Game The_Cycle:_Frontier"
            export ttvdropbot_autoclaim=true
        fi
        ./ttvdropbot
    fi
    sleep 10
done
```
