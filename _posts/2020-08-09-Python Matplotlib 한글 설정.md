---
title: Python Matplotlib 한글 설정
author: chhak
date: 2020-08-09 00:00:00 +0800
categories: [Python]
tags: [Python]
---

```
#패키지 설정
import matplotlib.font_manager as fm

#폰트 리스트 확인
font_list = fm.findSystemFonts(fontpaths=None, fontext='ttf')
font_list[:4]

#아무 폰트 선택후 인덱스 번호로 선택하여 이름 확인
a = fm.FontProperties(fname=font_list[3])
a.get_name()

#family에 해당 폰트이름을 넣기
rc('font', family="Magic R")
```
