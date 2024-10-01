---
title:  "How to use GitHub Pages?"
description: Sanya's first article
date:   2024-10-01 14:20:36 +0800
categories: [GitHub]
author: Sanya
tags: [GitHub]
---
# How to use gitHub pages to create your blog!  

## 環境及工具 ## 
- macOS Sonoma 14.6.1
- 環境語言：Ruby  
- 依賴管理工具：RubyGems.org、Bundler  
- 靜態網站引擎：Jekyll (Based on Ruby)  
- 文章格式：Markdown  
- 伺服器：Github Page (免費、無限流量/容量 靜態網站伺服器)  
- CI/CD：Github Action (免費 2,000 mins+/月)  
- 版本控制：Git  

## 安裝 Ruby ##
- rbenv
- ruby 3.3.5

**安裝 Brew**  
在 Terminal 輸入以上指令安裝 Brew
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
**安裝 rbenv**  
MacOS 雖自帶 Ruby 但建議使用 rbenv 安裝另一個 Ruby 與系統自帶的區隔開來，在 Terminal 輸入以上指令安裝 rbenv。
```
brew install rbenv ruby-build
```

在 Terminal 輸入以上指令初始化 rbenv  
```
rbenv init
```
關閉＆重新打開 Terminal  
在 Terminal 輸入rbenv 檢查是否安裝成功！  

![](../assets/post_images/2024-10-01-githubPages/check_rbenv.png)
成功！  

**使用 rbenv 安裝 Ruby**  
在 Terminal 輸入以上指令安裝 Ruby 3.3.5 版本  
```
rbenv install 3.3.5
```
在 Terminal 輸入以上指令將 Terminal 所使用的 Ruby 版本從系統自帶的切換到 rbenv 的版本  
```
rbenv global 3.3.5
```
在 Terminal 輸入 rbenv versions、ruby -v 查看當前 Ruby、gem -v 查看當前 RubyGems 設定  
![](../assets/post_images/2024-10-01-githubPages/check_gem.png)

*Ruby 安裝完後理應也安裝好 RubyGems了。

成功！

**安裝 Jekyll & Bundler**  
在 Terminal 輸入以上指令安裝 Jekyll & Bundler  
```
gem install jekyll bundler
```
完成！  

## 從模版建立 Jekyll Blog
預設的 Jekyll Blog 樣式非常簡潔，我們可以從以下網站找到自己喜歡的樣式並套用  

- [jekyll-theme](https://github.com/topics/jekyll-theme)  
- [jamstack Themes](https://jamstackthemes.dev/ssg/jekyll/)  
- jekyllthemes.org (http://jekyllthemes.org/)  
- [jekyllthemes.io](https://jekyllthemes.io/)  
- [jekyll-themes.com](https://jekyll-themes.com/)  
安裝方式一般使用 gem-based themes，也有的 Repo 提供 Fork 方式安裝；甚至是提供直接一鍵安裝方式；總之每個模板的安裝方式可能有所不同，請參閱模板的教學使用
  
這邊就以我 Blog 採用的模版 Chirpy 為示範，此模版提供最傻瓜的一鍵安裝方式，可以直接使用

**從 Git Template 建立 Git Repo**  
點擊以下連結建立repository到你的GitHub  
[Chirpy](https://github.com/cotes2020/chirpy-starter/generate)

![](../assets/post_images/2024-10-01-githubPages/create_repository.png)

- Repository name：Github帳號/組織名稱.github.io (務必使用這個格式)
- 務必選擇「Public」公開 Repo

點擊「Create repository」

完成 Repo 建立。  

**Git Clone 專案**  
git clone 剛剛建立的 Repo
```
git clone git@github.com:developer-tw/developer-tw.github.io.git
```
cd 到developer-tw.github.io資料夾，執行bundle安裝  
```
bundle
```
![](../assets/post_images/2024-10-01-githubPages/install_bundle.png)

執行 bundle lock — add-platform x86_64-linux 鎖定版本
![](../assets/post_images/2024-10-01-githubPages/bundle_lock.png)

**修改網站設定**  
打開 _config.yml 設定檔案進行設定  
請依照註解將設定替換成您的內容


**預覽網站**  
可以下 bundle exec jekyll s 啟動本地網站
```
bundle exec jekyll s
```
![](../assets/post_images/2024-10-01-githubPages/bundle_exec.png)

複製其中的網址 http://127.0.0.1:4000/ 貼到瀏覽器打開

![](../assets/post_images/2024-10-01-githubPages/preview_website.png)  
  
本地預覽成功！

## Jeklly 目錄結構  

![](../assets/post_images/2024-10-01-githubPages/jeklly_tree.png)  
文章目錄在
- _posts/：文章會放在這個目錄下
文章檔案命名規則：YYYY–MM–DD-文章檔案名稱.md
- assets/：
網站資源目錄，網站用圖片或文章內的圖片都要放置於此  

其他目錄 _incloudes、_layouts、_sites、_tabs… 都可讓你做進階的擴充修改

## 建立/編輯文章  
**使用 Visual Code**  
- 文章檔案命名規則：YYYY–MM–DD-文章檔案名稱.md  
- 建議以英文為檔案名稱 (SEO 最佳化)，這個名稱就會是網址的路徑  
  
**文章內容頂部**  
```
---
layout: post
title:  "How to use GitHub Pages?"
description: Sanya's first article
date:   2024-10-01 14:20:36 +0800
categories: Jeklly Life
author: Sanya
tags: [GitHub][Pages]
---
```

- layout: post  
- title: 文章標題 (og:title)  
- description: 文章描述 (og:description)  
- date: 文章發表時間 (不可以是未來)  
- author: 作者 (meta:author)  
- tags: 標籤 (可多個)  
- categories: 分類 (單個，用空格區分子母分類 Jeklly Life -> Jeklly 目錄下的 Life 目錄)  

**文章內容**   
使用 Markdown 格式撰寫  
```
# How to use gitHub pages to create your blog!  

## 環境及工具 ## 
- macOS Sonoma 14.6.1
- 環境語言：Ruby  
- 依賴管理工具：RubyGems.org、Bundler  
- 靜態網站引擎：Jekyll (Based on Ruby)  
- 文章格式：Markdown  
- 伺服器：Github Page (免費、無限流量/容量 靜態網站伺服器)  
- CI/CD：Github Action (免費 2,000 mins+/月)  
- 版本控制：Git  
```  

## 上傳內容到GitHub  
使用以下 Git 指令操作  
```
git add .
git commit -m "update post"
git push
```
    
      
        
          
            
              


> _有任何問題及指教歡迎 [與我聯絡](https://www.sanyaceo.com) 。_