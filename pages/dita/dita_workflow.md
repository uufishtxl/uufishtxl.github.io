---
title: DITA Work Process
catalog: true
tags: 
  - dita
permalink: dita_workflow.html
folder: dita
summary: Authoring-Reviewing & Commenting-Finalizing
---

## Authoring

Author directly using DITA to get habituated to the syntax.

## Reviewing & Commenting

1.  Generate webhelp output.
2.  Paste it onto Google Docs.
3.  Send the doc to engineers and ask them to make comments.
4.  Would you like to preserve the comments in your DITA source?  
    **If Yes**: You can do this in a couple of ways.
    -   ***Method 1***: Swtich to the Author view. Locate the **Comment** button on the top tool bar. Click it and type your comment on the prompt box.
        ![Comment in the Author view](/img/dita/dita_workflow_reviewing_btnComment.png)
    -   ***Method 2***: Switch to the Text view. Surround your suggestion within a pair of `<draft-comment author="yourName" time="mm/dd/yyyy">` tags.  
        Oxygen transformation defaults to omit comments. If you really want to output them, bring about the **Configure Transformation** dialog box, select the target engine and look for the parameter `args-draft`. Set its value to **Yes**.  
5.  Make the changes in the source DITA files and mark the comments as resolved on Google Docs.


## Finalizing

When you are done making all the changes, output a new version and replace the Google doc. This will not drop the previous comments.  
![Show All Comments on Google Doc](/img/dita/dita_workflow_reviewing_showAllComments.png)