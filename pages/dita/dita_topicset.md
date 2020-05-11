---
title: topicset
catalog: true
tags: 
  - dita
permalink: dita_topicset.html
folder: dita
summary: topicset, a collection of topics with a unique ID for re-use as a whole
---

## `topicset`

`topicset` contains several topics and can also take a unique ID to facilitate re-use as one topicset.

### Highs

To conflict the fear for information fragmentation.

### How-to

```XML
<topicset id="replacing_broken_spokes" navtitle="Replacing broken spokes" href="about_broken_spokes" chunk="to-content">
<topic href="remove_broken_spokes" toc="no"/>
<topic href="remove_the_cassette" toc="no" />
<topic href="replace_the_spoke_nipple" toc="no" />
<topic href="reattach_the_cassette" toc="no" />
</topicset>
```

In the example above, please note the attribute-value pairs s as below：

-   `chunk=“to-content”`: Merges all children topics to the same file;
-   `toc="no"`: Specified for each child topic, preventing it from appearing in the table of contents
-   `href="about_broken_spokes"`: This topic is an overview to all the subtasks. Get it nested under the `topicset` title rather than under its own subtitle. ***Don't quite understand what it means...***

### Lows

Though the topic renders as one unit, Oxygen's webhelp search engine surfaces each unit separately.




{% include note.html content="如果要引用的内容在其他文件夹中，必须在文件名前提供正确的路径。" %}



