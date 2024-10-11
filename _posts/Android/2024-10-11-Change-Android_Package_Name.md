---
title: AndroidStudio Change Package Name Tutorials
description: Introduction how to change package name
date: 2024-10-11 11:30:58 +0800
categories: [Android]
tags: [Android, Studio, Package]
---

# Change Package Name for AndroidStudio
如果你想修改Project的Package Name請依照以下步驟:

## 更改顯示Project結構方式

1. 將項目切換到Ａndroid
2. 點擊齒輪圖案
3. 然後將Compact Empty Middle Package 選項取消

![](../assets/post_images/2024-10-11-Change_Android_PackageName/unCheck_compact_empty.png)  

## 修改個別名稱
例如更改前的Package Name為 com.zzz.testing 
要更改為com.appliction.sanyaApp

1. 對需要修改的名稱上按右鍵，選擇refactor
   ![](../assets/post_images/2024-10-11-Change_Android_PackageName/select_refactor.png)  
2. 再選擇Rename，再按All Directory
   ![](../assets/post_images/2024-10-11-Change_Android_PackageName/select_rename.png)
3. 然後選擇Do Refactor
4. 再修改app build的applicationId，改成和我們之前修改的package name
   ![](../assets/post_images/2024-10-11-Change_Android_PackageName/change_applictionid.png)
5. 點擊Sync Now 
6. 按Build如果有問題再一一修正到正確的Package name
