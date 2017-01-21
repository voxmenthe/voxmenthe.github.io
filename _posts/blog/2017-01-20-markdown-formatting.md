---
layout: post
title: Markdown & HTML Practice & Notes
modified:
categories: blog/
excerpt:
tags: [markdown, github pages, web publishing]
image:
  feature:
date: 2017-01-20T09:15:45-00:00
---

#### In this post, I am simply noting down some of the very basic html and markdown recipes I'm using on this blog:

\| Left-aligned | Center-aligned | Right-aligned |
\| :---         |     :---:      |          ---: |
\| git status   | git status     | git status    |
\| git diff     | git diff       | git diff      |


| Left-aligned | Center-aligned | Right-aligned |
| :---         |     :---:      |          ---: |
| git status   | git status     | git status    |
| git diff     | git diff       | git diff      |


Code block in triple backtick quotes:
```
git status
git add
git commit
```
<style>
  .mytable 
  {
  background-color: #eee;
  border: 1px solid #999;
  display: block;
  padding: 20px;
  }
</style>

Code block using html type 1:
<code>
git status
git add
git commit
</code>

Code block using html table:
<table class="mytable">
<tr> 1: the code block that is supposed to go inside this table block </tr>
<tr> <td> 2: the code block that is supposed to go inside this table block </td> </tr>
</table>

pre code {
  background-color: #eee;
  border: 1px solid #999;
  display: block;
  padding: 20px;
}