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

## 試著跟語言模型聊天  
以下是第一個範例，該程式碼用一句簡單問句Hi, How are you today? 與語言模型Ollama進行互動

```
from langchain_community.llms import Ollama


llm = Ollama(model='llama2')
print(llm.invoke('Hi, how are you today?'))
```
上述程式執行之後，會回應以下結果
![](../assets/post_images/2024-10-04-LangChain-llama/first_program.png)

程式碼說明如下:
1. import Ollama 
2. Ollama(model='llama2') 利用Ollama載入llama2語言模型
3. 最後使用語言模型的invoke()方法，傳入我們想要與模型互動的字串，最後將結果列印出來

## 將操作變成Chain
學習 LangChain 最重要的就是將語言模型的操作變成 Chain  
Chain 的組合需要使用 | 運算子，都是將前一個指令的結果透過管道傳給下一個指令的作用。  
最簡單的Chain如下:
```
chain = prompt | llm
```
瞭解Chain之後我們將第一個範例轉為Chain的形式:
```
from langchain_community.llms import Ollama
from langchain_core.prompts import ChatPromptTemplate

llm = Ollama(model='llama2')

prompt = ChatPromptTemplate.from_messages([
    ("user", "{input}"),
])

chain = prompt | llm

print(chain.invoke({"input": "Hi, how are you today?"}))
```
程式碼說明如下:  
我們使用 langchain_core.prompts 模組中的 ChatPromptTemplate 定義 prompt，這組prompt只接受一個使用者輸入的參數 {input}，接著我們將 prompt 與 llm 透過 | 運算子組合成 chain，最後透過 chain 的 invoke 方法，將 input 參數代入。  
上述範例的執行結果如下:
![](../assets/post_images/2024-10-04-LangChain-llama/transfer_first2Chain.png)

從結果中我們可以發現多出了Assistant字串，我們需要對語言模型的輸出做額外的處理，例如去掉多餘字串或轉為其它格式等等，我們可以透過在Chain的尾端加入處理輸出的方式達成:
```
chain = prompt | llm | <處理輸出的程式>
```
(處理輸出的程式)在LangChain稱為output parser同時，LangChain也有內建一個class稱為StrOutputParser可以使用，因此可以透過繼承的方式做客製化的輸出處理，最簡單的客製化的程式碼如下所示：
```
class MyOutputParser(StrOutputParser):
    def parse(self, text):
        return text.replace('Assistant:', '')
```  
上述範例透過 override parse() 方法，達到去掉 Assistant: 字串的目的。  
完整範例如下:
```
from langchain_community.llms import Ollama
from langchain_core.output_parsers import StrOutputParser
from langchain_core.prompts import ChatPromptTemplate

class MyOutputParser(StrOutputParser):
    def parse(self, text):
        return text.replace('Assistant: ', '')

output_parser = MyOutputParser()

llm = Ollama(model='llama2')
prompt = ChatPromptTemplate.from_messages([
    ("user", "{input}"),
])

chain = prompt | llm | output_parser
print(chain.invoke({"input": "Hi, how are you today?"}))
```

執行結果會發現 Assistant: 消失了
![](../assets/post_images/2024-10-04-LangChain-llama/remove_string.png)

## 語言模型系統指令  
學會Chain的用法之後，就可以為語言模型做些加值應用，例如賦予它系統指令，例如請它扮演一個具有SEO知識的專業寫手，幫助我們寫一些文章。  
要賦予它系統指令，就需要在 prompt 著手，加上系統指令，系統指令的格式為：
```
("system", "系統指令")
```
以剛剛的 SEO 專業寫手為例，系統指令可以寫成
```
("system", "You are a content manager with extensive SEO knowledge. Your task is to write an article based on a given title.")
```

接著，將系統指令放到 prompt 中：
```
from langchain_community.llms import Ollama
from langchain_core.prompts import ChatPromptTemplate
from langchain_core.output_parsers import StrOutputParser

class MyOutputParser(StrOutputParser):
    def parse(self, text):
        return text.replace('Assistant: ', '')

output_parser = MyOutputParser()

llm = Ollama(model='llama2')

prompt = ChatPromptTemplate.from_messages([
    ("system", "You are a content manager with extensive SEO knowledge. Your task is to write an article based on a given title."),
    ("user", "{input}"),
])

chain = prompt | llm | output_parser
print(chain.invoke({"input": "Hi, how to remember english vocabulary?"}))
```

執行以上範例之後，會產生一篇文章如何記單字，如下:
![](../assets/post_images/2024-10-04-LangChain-llama/generate_article.png)

## 總結
本文的內容簡單介紹LangChain的大致樣貌，並且學會如何使用LangChain以及組合出Chain跟使用系統指令，現在應該都有能力能夠做出僅供自己使用的AI工具。

## 參考
[https://python.langchain.com/docs/get_started/introduction](https://python.langchain.com/docs/get_started/introduction)