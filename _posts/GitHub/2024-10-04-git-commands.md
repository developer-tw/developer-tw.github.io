---
title: Git Commands Tutorials
description: Introduction to Git Commands and usage
date: 2024-10-04 10:16:58 +0800
categories: [GitHub]
tags: [git]
---
# Git 指令介紹
## 常用指令列表

| 指令名稱                             | 指令內容                                                               |
| :----------------------------------- | :--------------------------------------------------------------------- |
| git init                             | 安裝 Git，會產出一個叫做 .git 的資料夾                                 |
| git add / git add .                  | 將檔案加入暫存區 / 將所有檔案加入暫存區 ( 切記新增的檔案必使用 )       |
| git commit -m "" / git commit -am "" | 將檔案加入倉庫區　/ 將檔案加入暫存並加入倉庫區，" " 內中請輸入訊息     |
| .ignoregit                           | 這不是指令而是文件名稱，把不要被 git 管控的檔案加入其中                |
| git status                           | 看目前 Git 管控中的檔案狀態                                            |
| git log                              | 看所有的 Commit 紀錄，後面加入 --oneline 可以看簡化版本的紀錄          |
| git diff                             | 比較檔案修改前後的不同，後面接兩組 commitID 可以看到兩組之間的差別     |
| git branch                           | 看目前的 branch 分支，與後面加參數 -v 相同，後面接名稱可以建立該名稱的 |
| git branch -d / git branch -D        | 刪除該 branch，-D 可以強制刪除未 merge 過的branch                      |
| git checkout                         | 切換到該 branch                                                        |
| git checkout -b xxx                  | 建立並切換到該 xxx branch                                              |
| git merge                            | 將該 branch 拉回融合至現下的 branch                                    |
| git remote                           | 使用 git remote origin master 連線到該 repo                            |
| git remote -v                        | 看當下連接的 GitHub                                                    |
| git pull                             | 將 Github 的 repo 拉下來 ( 下載 )，預設通常為 git pull origin master   |
| git push                             | 上傳，後面接該 branch 的名稱                                           |
| git reset HEAD                       | 取消被 add 至暫存區的檔案 branch                                       |
| git commit --amend                   | 取消上一個 commit                                                      |

<br>

## 常用指令介紹  
- 本地所有修改的。没有的提交的，都返回到原来的状态。
```
git checkout .          #本地所有修改的。没有的提交的，都返回到原来的状态
```
<br>

- 把所有沒有提交的修改暫存到stash裡面，可用git stash pop回復。
```
git stash               #把所有沒有提交的修改暫存到stash裡面
git pop                 #回復
```
<br>

- 返回到謀個節點，不保留修改，已有的改動會遺失。
```
git reset --hard HASH   #返回到謀個節點，不保留修改，已有的改動會遺失
```
<br>

- 返回到謀個節點，保留修改，已有的改動會保留，在未提交中，git status或git diff可看。
```
git reset --soft HASH   #返回到謀個節點，不保留修改，已有的改動會遺失
```
<br>

- 返回到謀個節點，未跟踪文件的删除。  
```
git clean -df           #返回到謀個節點，未跟踪文件的删除
git clean 参数 
    -n 不實際刪除，只是進行演練，展示將要進行的操作，有哪些文件將要被删除。（可先使用該命令参数，然后再决定是否執行）
    -f 删除文件
    -i 顯示將要删除的文件
    -d 遞迴删除目錄及文件（未跟踪的）
    -q 僅顯示錯誤，成功删除的文件不顯示
```
<br>

- clean與reset差異性
```
git reset               #删除的是已跟踪的文件，将已commit的回退
git clean               #删除的是未跟踪的文件
git clean -nxdf         #查看要删除的文件及目錄，確認無誤後再使用下面的命令進行删除
git checkout . && git clean -xdf 
```
<br>

- 打包patch跟打patch
```
git format-patch 5e86795..f2b286a   #從指定起始commit到結束commit的patch
git am 0001-modify-page.patch       #再下git am指令前記得要先下git am --abort
```
<br>

- Cherry-pick用法
  <br>
  [同倉庫](https://cythilya.github.io/2018/05/30/git-cherry-pick/)
  ```
  git cherry-pick 5edd113 5a0ffbc -n  (將5edd113 與5a0ffbc兩個commit 合入分支, -n 接到當前branch後面)
  git status
  git commit -m "合併 B、C 功能"
  git push origin master
  ```
  [不同倉庫](https://www.jianshu.com/p/1441288e3ab2)
  ```
  # 將另外一個分支加到遠端分支
  git remote add proj https://分支地址.git
  # 拉取遠端倉庫的數據
  git fetch proj


  # 合併指定的提交，後面是另一個分支的提交Hash
  git cherry-pick sjfdishudf877s8df7sdf
  git cherry-pick fidfjiuhisdu87sdhf7yf
  git push
  ```
<br>

- 抓特定commit 版本  
使用 git checkout -b branch_name commit_id 在指定的 patch 上建立新的 branch 並且切換過去  
```
git checkout -b branch_name e87a289
```
<br>

- 子模組
  [參考](https://blog.kennycoder.io/2020/06/14/Git-submodule-%E4%BD%BF%E7%94%A8%E6%95%99%E5%AD%B8/)  
  **用法**  
  ```
  git submodule add <remote repository> <local path>

  remote repository 就是要填你的子 Repository 的 URL，local path 指的是你要放在本地端主 Repository 的路徑位置
  ```
  **示範如下**:
  ```
  git submodule add https://github.com/KennyChenFight/git-sub-module.git reference/git-sub-module
  ```
    - 請注意，這是我們在前面建立子 Repository 的 URL，而後面代表的是自動創立 reference/git-sub-module 這個資料夾，而裡面就會放子 Repository 的專案內容
    - 接著，我們對主 repository 進行 push 的動作，看遠端的 repository 會怎樣去連接子模組  
        git add .  
        git commit -m "add submodule"  
        git push  

  **子模組更新內容**   
  我們在本地端對子模組進行新的內容更改，並 push 到 remote repository  
  ```
  cd git-sub-module
  echo "update submodule content" >> sub.txt
  git add .
  git commit -m "update content"
  git push
  ```

  **主模組這邊的子模組同步更新**  
  這邊轉移到本地端 git-main-module 主模組這邊進行子模組的更新   
  ```
  cd git-main-module
  ```
  拉取主子模組remote的更新內容，並且與master進行merge  
  ```
  git submodule update --remote --merge
  ```
  這時候就可以把更新內容 push 上去到主模組那邊，讓 remote 那邊的子模組也可以指到新的內容  
  ```
  git add .
  git commit -m "update submodule"
  git push
  ```
  **主子模組整個都要更新**  
  ```
  git pull --recurse-submodules <branch>
  ```
  **Clone 主子模組**  
  ```
    1. git clone <remote_url>
       git submodule update --init --recursive
       git clone --recurse-submodules <remote_url>

    2. git clone --recursive <url>
    
    3. 如果已經抓下來才發現submodule是空的，可以用以下指令去抓，init 會在 _.git/config` 下註冊 remote repo 的 URL 和 local path：
       git submodule init
       git submodule update --recursive   
  ```
  **如何刪除 Git Submodule 的關係**  
  ```
  # 在主模組目錄下解除submodule關係
    git submodule deinit reference/git-sub-module  

  # 刪除在.gitmodules檔案的與git-sub-module的內容
    git add .gitmodules
    git rm --cached reference/git-sub-module  

  # 這個路徑下的所有檔案刪除
    rm -rf .git/modules/reference/git-sub-module
    git commit -m 'remove submodule'
    rm -rf reference/git-sub-module
    git push
  ```

## 多帳號使用不同 ssh key 設定指南
在 Github 上不同的帳號之間是不能共用公鑰的，所以假如在一台電腦中同時要給兩個 Github 帳號使用的話，
因為是同個 domain 所以需要特別調整設定，本篇將教學如何調整。
1. 首先要先設定 ~/.ssh/config 
    假設在 Github 上有兩個帳號分別為 **eys3d** 與 **developer-tw**，而對應的 key 如下：
    - eys3d 的 key 是在 ~/.ssh/id_rsa
    - developer-tw 的 key 是在 ~/.ssh/id_rsa_developer-tw  

    這時要在 ssh config (位置：~/.ssh/config) 中設定如下：
    ```
    Host github.com-eys3d
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_rsa

    Host github.com-developer-tw
        HostName github.com
        User git
        IdentityFile ~/.ssh/id_rsa_developer-tw
    ```
2. 對想要使用的 project 進行 clone
    假設現在想要 clone 的 repo url 是 git@github.com:demo/project-a.git  
    這時只需要將 github.com 替換成 github.com-eys3d 或是 github.com-developer-tw 就能夠使用不同的 key 跟身分進行連線  
    例如以下的方式就是使用 github.com-eys3d 的 key 進行 clone：
    ```
    git git@github.com-eys3d:demo/project-a.git
    
    真實範例:
    git clone git@github.com-ethanwu118:ethanwu118/object_detector.git
    ```

## 修改了檔案或刪錯檔案了，還沒commit前，後悔了怎麼辦?
- 修改檔案或刪除檔案 filename.txt，但後悔了
```
git checkout filename.txt   #還原已修改或已刪除檔案(常用)
git checkout                #還原 目錄 
git checkout master         #還原 分支(master)之內所有檔案
```  
- 檔案 filename.txt 修改，並且已經add
```
git reset --HARD            #退到修改或刪除前 (常用)
git reset --soft            #退到 staging   (已add 但未commit)
git reset --mixed           #退到 untrack  (還沒add)
```   
  
## 修改了檔案或刪錯檔案了，已經commit了，後悔了怎麼辦?
以下針對已經commit 的還原方式
<br>
```
新增 dog.txt  commit   #aa00
刪除 dog.txt  commit   #aa01
```
首先先git log 顯示 commit 歷程，找到想還原的commit編號，例如:#aa00
```
git reset --hard aa00       #回到該commit編號(常用)
  
若還原檔案後(aa00)又後悔，想再回到原本的commit (aa01 )
用git log 已經看不到該commit編號(aa01)，因為已經回到從前(aa00)了
請改用git reflog 找到 aa01
git relog
git reset --hard aa01       #回到該commit編號(常用)
```
