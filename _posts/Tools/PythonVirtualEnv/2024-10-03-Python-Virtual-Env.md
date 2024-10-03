---
title:  "Virtual Python Environment"
date:   2024-10-03 14:20:36 +0800
categories: [Tools, PythonVirtualEnv]
author: Sanya
tags: [python]
---
# How to create a virtial python vnvironment

## 環境及工具 ## 
- macOS Sonoma 14.6.1
- python 3.9.6
  
## 建立新的虛擬環境
**建立新資料夾**  
```
mkdir python_env
```
進去你剛建的資料夾  
```
cd python_env
```
建立虛擬環境  
```
python3 -m venv virtual_env
```
virtual_env 是虛擬環境的名稱，可以隨便取，一樣不要有中文或奇怪符號。按下 enter 後會小等一下，接著輸入 ls 來顯示這個資料夾裡面有什麼，如圖，現在裡面有你的虛擬環境囉  

![](../assets/post_images/2024-10-03-pythonEnv/python_ls.png)  

以上就是 2.1 建立新的虛擬環境，目前只有建立，接下來要介紹啟動。  

## 啟動已建立虛擬環境的SOP  
**啟動虛擬環境**  

```
source virtual_env/bin/activate
```

**確認有沒有啟動**   

![](../assets/post_images/2024-10-03-pythonEnv/python_check_active.png)  

如圖，最前面會出現(virtual_env)，代表你已經在這個虛擬環境中。  
  
輸入 which python3 ，會得到你現在使用的python3是從哪來的，而顯示的就會是你虛擬環境的地址  
  
![](../assets/post_images/2024-10-03-pythonEnv/which_python3.png)  

## 查看已有哪些套件  

pip3 list 可以顯示出你目前這個虛擬環境中有哪些套件。如圖，最原始版本只有pip和setuptools。下一步我們來安裝吧！  

![](../assets/post_images/2024-10-03-pythonEnv/pip_list.png)  

**安裝套件**  

以下整理基本上一定會用到的套件  
```
pip install pandas
pip install numpy
pip install matplotlib
pip install jupyterlab
pip install seaborn
pip install — upgrade tensorflow
pip install scikit-learn
pip install Keras
```  
## 關閉虛擬環境  
假設你是用jupyter notebook 或是 jupyter lab，結束的時候要先在terminal輸入 control⌃+c 終止jupyter，接著輸入 deactivate 來關閉虛擬環境。  
如下圖最前面(virtual_env)消失了，那就代表你關閉虛擬環境了
  
```
deactivate
```  
   

![](../assets/post_images/2024-10-03-pythonEnv/deactivate.png)  


## 懶人包

**建立虛擬環境**  

```
cd /Users/你的電腦名稱/Documents #到你要的資料夾
mkdir newfolder_name #新增資料夾
cd newfolder_name #進到資料夾
python3 -m venv name_env #建立虛擬環境
```  

**開啟虛擬環境SOP**  
```
cd /Users/你的電腦名稱/Documents/newfolder_name #到有虛擬環境的資料夾
source name_env/bin/activate #開啟虛擬環境
jupyter lab #開啟jupyter lab，接著就可以開始使用
```  

**關閉虛擬環境**  
```
deactivate
```  