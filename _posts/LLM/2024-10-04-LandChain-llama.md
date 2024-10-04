---
title: LangChain With Meta llama2 Model Tutorials
description: Introduction LangChain llama
date: 2024-10-04 16:36:58 +0800
categories: [LLM]
tags: [LLM, LangChain, Meta, llama2]
---
# LangChain 入門教學
> 本文將介紹 LangChain 結合 llama 語言模型如何使用的入門教學  

p.s. 使用開源語言模型的 llama 的好處在於不用付費，輸出品質也有一定保證
<br>

## 環境需求
- macOS
- Python 3
- LangChain
- Ollama

## 安裝虛擬Python環境 
[請參考這篇文章](https://developer-tw.github.io/posts/Python-Virtual-Env/)

## 安裝工具
首先安裝LangChain Framework。
<br>
```
pip install langchain
```
本文需要 Ollama 指令與 Meta 公司提供的 llama2 模型(model)，ollama 指令請至 [Ollama](https://ollama.com/download) 官方頁面下載安裝，
安裝完成之後即可執行指令安裝 llama2 模型，其安裝指令如下：
<br>
```
ollama run llama2
```
<br>

## LangChain 簡介
LangChain 是一套專門用來開發語言模型(Language Model)相關應用的框架(framework), 簡單來說可以讓開發者整合不同的語言模型，開發像 ChatGPT, ChatBox 聊天機器人、數位助理等等應用程式。可以參考[LangChain](https://python.langchain.com/docs/introduction/)介紹。

- Lang 代表 Language Model，也是呼應 LangChain 專門用以開發語言模型相關應用的用途。

- Chain 的部分則是 LangChain 的功能，它將大語言模型的應用視為一個 Chain，舉 ChatGPT 聊天應用為例，它至少需要結合提示詞(prompt)與一個大語言模型，過程很像是把提示詞丟給大語言模型處理，例如：
  > 提示詞："你是個資深工程師，請幫我寫出一個 Python Hello World 範例"  
  > 大語言模型


  這樣的組合行為在 LangChain 被抽象化為一個 Chain，程式碼片段如下：
  ```
  from langchain_openai import ChatOpenAI
  from langchain_core.prompts import ChatPromptTemplate

  llm = ChatOpenAI(openai_api_key="...省略...")
  prompt = ChatPromptTemplate.from_messages([
    ("system", "你是個資深工程師"),
    ("user", "請幫我寫出ㄧ個 Python Hello World 範例")
  ])

  chain = prompt | llm
  ```
上述範例中的 prompt | llm 就是ㄧ個最簡單的 Chain，所以開發 LangChain 應用其實多半是在組合/處理 Chain 的工作，讓 Chain 能夠藉由語言模型的力量提供服務。
這個組合方式稱為 LCEL, LangChain Expression Language 。

<br>

**LangChain框架由以下開源庫組成:** 
- langchain-core: 基礎抽象層與LangChain表達語言.
- langchain-community: 第三方集成.
  - 合作包（例如 langchain-openai，langchain-anthropic 等）：一些集成被進一步拆分為只依赖於 langchain-core 的輕量級包.
- langchain: 組成應用程式認知架構的鏈、代理和檢索策略.
- LangGraph: 通過將步驟建模為圖中的邊和節點，建構穩健且有狀態的多角色應用程序。可以LangChain無縫集成，也可以獨立使用.
- LangServe: 將LangChain鏈部署為REST API.
- LangSmith: 一個開發者平台，允許你調試、測試、評估和監控LLM應用程序.

![](../assets/post_images/2024-10-04-LangChain-llama/LangChain_framework.png)
[圖片引用來源 - LangCain 官網](https://python.langchain.com/docs/introduction/)
