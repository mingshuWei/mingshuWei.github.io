---
layout:     post
title:      Android bitmap 高效使用
subtitle:   bitmap
date:       2018-09-01
author:     mingshu
catalog: true
tags:
    - bitmap
    - Android
---
# Bitmap 高效实用

## Bitmap 压缩

## 后台加载

## Cache 缓存
两级cache 
1. memory cache
有人习惯使用SoftReference 和 WeakReference 来做Memory cache，但是谷歌官方不建议这么做，因为android 2.3之后，android 中gc 变得更加频繁
2. disk cache