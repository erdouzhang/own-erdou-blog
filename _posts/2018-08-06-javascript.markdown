---
layout:     post
title:      "《Javascript高级程序设计》(一)"
subtitle:   " \" 延迟脚本和异步脚本\""
date:       2018-08-06 20:15:00
author:     "Erdou"
header-img: "img/post-bg/post-bg-2018.jpg"
catalog: true
tags:
    - javascript
---

> “Yeah It's on. ”


### 延迟脚本(defer)

脚本执行时，不会影响页面的构造。整个页面都解析完成后再执行，立即下载，延迟执行。脚本会优先于DOMContentLoaded事件执行（不一定）。

---

### 异步脚本(async)
用于改变处理脚本的行为，浏览器立即下载文件。异步脚本不要在加载期间修改DOM。异步脚本一定会在页面的load事件前执行，但是可能会在DOMContentLoader事件触发前或触发后。

---
