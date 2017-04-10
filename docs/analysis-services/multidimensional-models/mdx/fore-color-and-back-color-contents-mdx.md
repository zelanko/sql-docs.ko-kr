---
title: "FORE_COLOR 및 BACK_COLOR 내용(MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FORE_COLOR 내용"
  - "배경 [MDX]"
  - "셀 [MDX]"
  - "색상 [MDX]"
  - "셀 색상 정보 저장"
  - "셀 배경"
  - "BACK_COLOR 내용"
ms.assetid: ff8f40cb-2ac4-4fc2-9761-7f1b14c17c8c
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# FORE_COLOR 및 BACK_COLOR 내용(MDX)
  **FORE_COLOR** 및 **BACK_COLOR** 셀 속성은 셀의 텍스트 및 배경의 색 정보를 Microsoft Windows 운영 체제의 RGB(Red-Green-Blue) 형식으로 저장합니다.  
  
 일반적인 RGB 색의 유효 범위는 0부터 16,777,215(&H00FFFFFF)까지입니다. 이 범위에 속하는 숫자의 상위 바이트는 항상 0이며 최하위부터 최상위에 이르는 하위 3바이트가 빨간색, 녹색, 파란색의 양을 결정합니다. 빨간색, 녹색, 파란색 구성 요소는 각각 0부터 255(&HFF) 사이의 숫자로 표시됩니다.  
  
## 관련 항목:  
 [셀 속성 사용&#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/using-cell-properties-mdx.md)  
  
  