---
title: Reusing Content
catalog: true
tags: 
  - dita
permalink: dita_reuse.html
folder: dita
summary: 利用topicref和conref来重用内容
---

## conref

1.  建立一个重用库，比如说`snippets.dita`，ID是`note123` 。


2.  在重用库中，赋予要引用的内容一个独一无二的`id`。

    ```
    <note type="warning" id="tightening_warning">Do not...</note>
    ```

3.  在别的主题中引用该内容时，需要：

    -   确保与要引用的内容属于同一种标签
    -   在该标签中，用`conref`属性来指定引用目标，格式是`<labelName conref="library.dita#libraryId/conotentId">`

        ```
        <note conref="snippets.dita#note123/tightening_warning">
        ```

    {% include note.html content="如果要引用的内容在其他文件夹中，必须在文件名前提供正确的路径。" %}

## `topiref`的属性`processing-role`

在`ditamap`中，引用`topicref`时，有一个属性叫做`processing-role`，当设置为`processing-role="resource-only"`时，只会将该主题包含到这个map中，而不会显示到输出文件中。

