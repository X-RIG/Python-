# python笔记

requests.get(uri,params=None,**kwargs)

url:所需获取页面的url链接

params：url中的额外参数，字典或字节流格式

**kwargs：12个控制访问的参数

|        属性         |                       说明                       |
| :-----------------: | :----------------------------------------------: |
|    r.status_code    |      HTTP请求的返回状态 200为成功 404为失败      |
|       r.text        |  HTTP相应内容的字符串形式，即url对应的页面内容   |
|     r.encoding      |      从http header中猜测的相应内容编码方式       |
| r.apparent_encoding | 从内容中分析出的相应内容编码方式（备选编码方式） |
|      r.content      |             HTTP相应内容的二进制形式             |

**通用代码框架**

```python
def getHTMLText(url):
    try :
        r = requests.get(url, timeout=30)
        r.raise_for_status()
        r.encoding = r.apparent_encoding
        return r.text
    except:
        return "产生异常"
```

|        方法         |                  说明                  |
| :-----------------: | :------------------------------------: |
| requests.requests() | 构造一个请求，支撑一下各方法的基础方法 |
|   requests.get()    | 获取HTML网页的主要方法，对应HTTP的GET  |
|   requests.head()   |        获取HTML网页头信息的方法        |
|   requests.post()   |      向HTML网页提交post请求的方法      |
|   requests.put()    |      向HTML网页提交put请求的方法       |
|  requests.patch()   |       向HTML网页提出局部修改请求       |
|  requests.delete()  |           向HTML网页删除请求           |

 字典是 Python 提供的一种常用的数据结构，它用于存放具有映射关系的数据。

### **kwargs

**params**  字典或字节序列，作为参数增加到url中

**data**  字典、字节序列或文件对象，作为request的内容

**json**  JSON格式的数据，作为request的内容

**headers**  字典，HTTP定制头

---

**cookies**  字典或CookieJar，Request中的cookie

**auth**  元祖，支持http认证功能

**files**  字典类型，传输文件

**timeout**  设定超时时间，s为单位

**proxies**  字典类型，设定访问代理服务器，可以增加登录认证

**allow_redirects**  True/False，默认为True，重定向开关

**stream**  True/False，默认为True，获取内容立即下载开关

**verify**  True/False，默认为True，认证SSL证书开关

**cert**  本地SSL证书路径



### request方法

request.get(url,params=None,**kwargs)

request.head(url,**kwargs)

 request.post(url,data=None,json,None,**kwargs)

request.put(url,data=None,**kwargs)

request.patch(url,data=None,**kwargs)

request.delete(url,**kwargs)



## Beautiful Soup

html——标签树——BeautifulSoup类

|      解析器      |             使用方法              |         条件         |
| :--------------: | :-------------------------------: | :------------------: |
| bs4的HTML解析器  | BeautifulSoup（mk,'html.parser'） |      安装bs4库       |
| lxml的HTML解析器 |    BeautifulSoup（mk,'lxml'）     |   pip install lxml   |
| lxml的XML解析器  |     BeautifulSoup（mk,'xml'）     |   pip install lxml   |
| html5lib的解析器 |  BeautifulSoup（mk,'html5lib'）   | pip install html5lib |

| 基本元素        | 说明                                                    |
| --------------- | ------------------------------------------------------- |
| Tag             | 标签，最基本的信息组织单元，分别用<>和</>表明开头和结尾 |
| Name            | 标签的名字，<p>...</p>的名字是‘p’，格式是<tag>.name     |
| Attributes      | 标签的属性，字典形式组织，格式：<tag>.attrs             |
| NavigableString | 标签内非属性字符串,<>...</>中字符串，格式<tag>.stringnb |
| Comment         | 标签内字符串的注释部分，一种特殊的comment类型           |

例子：

```python
import requests
r = requests.get("http://python123.io/ws/demo.html")
demo = r.text
```

![](C:\Users\LENOVO\Desktop\python\Snipaste_2020-02-06_14-49-17.png)

标签树的下行遍历

|     属性     |                          说明                           |
| :----------: | :-----------------------------------------------------: |
|  .contents   |        子节点的列表，将<tag>所有儿子节点存入列表        |
|  .children   | 子节点的迭代类型，与.contents类似，用于循环遍历儿子节点 |
| .descendants |  子孙节点的迭代类型，包含所有子孙节点，用于循环遍历。   |

标签树的上行遍历

| 属性     | 说明                                         |
| -------- | -------------------------------------------- |
| .parent  | 节点的父亲标签                               |
| .parents | 节点先辈标签的迭代类型，用于循环遍历先辈节点 |

html是文本中最高级别的标签，所以它的父亲标签就是他自己。

标签树的平行遍历

| 属性               | 说明                                                 |
| ------------------ | ---------------------------------------------------- |
| .next_sibling      | 返回按照HTML文本顺序的下一个平行节点标签             |
| .previous_sibling  | 返回按照HTML文本顺序的上一个平行节点标签             |
| .next_siblings     | 迭代类型，返回按照HTML文本顺序的后续所有平行节点标签 |
| .previous_siblings | 迭代类型，返回按照HTML文本顺序的前续所有平行节点标签 |

```python
for sibling in soup.a.next_siblings:
	print(sibling)  #遍历后续节点

for sibling in soup.a.previous_siblings:
	print(sibling)  #遍历前续节点
```

![](C:\Users\LENOVO\Desktop\python\Snipaste_2020-02-07_10-18-16.png)



## 信息标记的三种形式

XML：是一种用尖括号，标签标记信息的表达形式 

JSON：是一种用有类型的键值对标记信息的表达形式

YAML：是一种用无类型的键值对标记信息的表达形式



## 提取信息

```python
from bs4 import BeautifulSoup
soup = BeautifulSoup(demo,"html.parser")
for link in soup.find_all('a'):
    print(link.get('href'))
```

### find_all

