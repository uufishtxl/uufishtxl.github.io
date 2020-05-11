---
title: DITA Basics
catalog: true
tags: 
  - dita
permalink: dita_basics.html
folder: dita
summary: DITA基础知识整理
---

## 为什么偏爱 Concept Topic?

Concept Topics:

| Have sections | √ |
| Accept numbered and ordered lists | √ |

## DITA的文件结构怎么安排比较好？

root  
root ditamap (includes maprefs to each sub-ditamap)  
 - folder
      - ditamap_1
      - topic_a
      - topic_b
      - topic_c

 - folder
      - ditamap_2
      - topic_d
      - topic_e
      - topic_f
 - folder
      - ditamap_3
      - topic_g
      - topic_h
      - topic_i
 - folder
      - snippets
      - keyrefs

### `ditamap`的位置

`ditamap`必须在它引用的文件的同级或上级文件夹，这是因为DITA不支持使用`../`来找寻上级文件夹。

不过Oxygen提供了一个折中的方法，来打破`../`的限制。具体的做法是：

1.  打开`Configure Transformation Scenario(s)`对话框。
2.  找到具体的Scenario，然后点击**Edit**。
3.  打开**Parameters**标签，找到`fix.external.refs.com.oxygenxml`，将它的值从`false`改成`true`。

## Handling Links

借助`keyref map`,使用有意义的词语来关联链接。

## 重用内容

可以通过两种元素进行重用：

- `topicref`，顾名思义，就是整个主题的重用
- `conref`，重用主题中的一段文字

Tom的做法是：将所有会重用的内容片段整理到同一个主题文件 (`ditabase`)。`ditabase`虽然不适用于撰写一般内容的主题，但是却拥有极高的兼容性，在内容的类型和多少上都不作限制，可以包含`task`、`reference`、`concept`。这么一个`ditabase`主题文件可以命名为`snippets.dita`，ID可以是`#note123`之类的。
