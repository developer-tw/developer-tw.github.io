---
title: Often Use Commands
description: Introduct Some Often Use Commands Including Git, Linux, and Android. 
date: 2024-10-15 10:01:18 +0800
categories: [Tools, OftenUseCommands]
tags: [command, linux, git]
math: true
---
# 常用指令
> 本文將介紹一些常用的指令包含Ａndroid、Linux、Git ,and so on。

## Android 

| 指令                                              | 說明                                           |
| :------------------------------------------------ | :--------------------------------------------- |
| adb devices                                       | 顯示連接到計算機的設備                         |
| adb get-serialno                                  | 獲取設備的ID與序列號 serial number             |
| adb reboot                                        | 重啟設備                                       |
| adb reboot bootloader                             | 重啟到bootloader 刷機模式                      |
| adb reboot recovery                               | 重啟到recovery 恢復模式                        |
| adb -d command                                    | 發送命令給usb連接的設備                        |
| adb -e command                                    | 發送命令到模擬器設備                           |
| adb -s serialNumber command                       | 發送命令到指定設備 需給定serial number         |
| adb kill-server                                   | 終止adb服務                                    |
| adb start-server                                  | 重啟adb服務                                    |
| adb root                                          | 以root權限重啟adb服務                          |
| adb wait-for-device                               | 在模擬器/裝置連線前把指令轉載在adb的指令器中   |
| adb shell  cat /sys/class/net/wlan0/address       | 取得mac位址                                    |
| adb shell cat /proc/cpuinf                        | 取得cpu序號                                    |
| aapt d badging <apkfile>                          | 取得apk的packagename 和 classname              |
| adb install <apkfile>                             | 安裝APK                                        |
| adb install -r <apkfile>                          | 保留資料和快取文件，重新安裝apk                |
| adb install -s <apkfile>                          | 安裝apk到sd卡                                  |
| adb uninstall <package>                           | 解除安裝app                                    |
| adb uninstall -k <package>                        | 卸載app但保留資料和快取文件                    |
| am start -n <package_name>/.<activity_class_name> | 啟動應用                                       |
| top                                               | 查看設備cpu和記憶體佔用情況                    |
| top -m 6                                          | 查看佔用記憶體前6的app                         |
| top -n 1                                          | 刷新一次記憶體訊息，然後返回                   |
| procrank                                          | 查詢各進程記憶體使用情況                       |
| kill [pid]                                        | 殺死一個進程                                   |
| ps                                                | 查看進程列表                                   |
| ps -x [PID]                                       | 查看指定進程狀態                               |
| service list                                      | 查看後台services資訊                           |
| cat /proc/meminfo                                 | 查看目前記憶體佔用                             |
| cat /proc/iomem                                   | 查看IO記憶體分區                               |
| ls                                                | 列出目錄下的文件和資料夾，等同於dos中的dir指令 |
| cd                                                | 進入資料夾，等同於dos中的cd 指令               |
| rename                                            | 重新命名文件                                   |
| rm                                                | 刪除                                           |
| mv                                                | 移動檔案                                       |
| chmod                                             | 設定檔案權限                                   |
| mkdir                                             | 新建資料夾                                     |
| cat                                               | 查看文件內容                                   |
| su                                                | 取得管理員權限                                 |
| adb remount                                       | 將system分區重新掛載為可讀寫分區               |
| adb pull <remote> <local>                         | 取得模擬器中的文件                             |
| adb push <local> <remote>                         | 向模擬器中寫入文件                             |
| android list targets                              | 顯示系統中全部Android平台                      |
| android list avd                                  | 顯示系統中全部AVD(模擬器)                      |
| mksdcard 1024M ~/名稱.img                         | 創建SDCard                                     |
| ddms                                              | 啟動DDMS                                       |
| adb -s 模擬器編號指令                             | 對某一模擬器執行指令                           |
| adb shell                                         | 進入模擬器的shell模擬                          |
| adb uninstall apk包的主包名                       | 卸載apk包                                      |
| adb help                                          | 查看adb指令幫助訊息                            |
| adb logcat -s 標籤名                              | 在命令列中查看log訊息                          |
| adb bugreport                                     | 查看bug報告                                    |

## Linux
- install deb file
  ```
  sudo dpkg -i *.deb
  ```
- file root
  ```
  sudo nautilus
  ``` 
- zip or unzip file
  ```
  tar -czvf 壓縮檔名稱.tgz 來源檔案
  tar -xzvf 壓縮檔名稱.tgz
  ```  
- change owner of file
  ```
  sudo chown myuser:mygroup myfile
  sudo chown -h myuser:mygroup myfile  //for ln only
  ```
- check library format
  ```
  file xxx.so
  readelf -h libsrtp.a
  readelf -Ws libz.so
  readelf -s libgio-2.0.so|grep g_module
  nm -gDC yourLib.so
  objdump -TC libz.so
  ```  

## Git
```
git log --oneline -n             // (n 是最近幾多次的提交記錄)
git reset --hard HEAD            // 回復到最新提交版本
git reset --hard HEAD~           // 等於 ~1 回復到上一個提交版本
git reset --hard HEAD~n          // n 等於往上第幾個提交版本 回復之前指定的提交版本
git reflog                       // 查看所有訊息版本
git reset --hard commit_id       // 根據 commit id 回覆到指定版本
```

