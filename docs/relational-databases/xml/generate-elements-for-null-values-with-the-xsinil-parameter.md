---
title: "XSINIL 매개 변수를 사용하여 NULL 값 요소 생성 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-xml"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "FOR XML 절, Null 값"
  - "Null 값 [SQL Server], XML"
  - "ELEMENTS 지시어"
  - "XSINIL 매개 변수"
ms.assetid: 2dbc4e48-1cae-4d83-b371-3265da9687cc
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# XSINIL 매개 변수를 사용하여 NULL 값 요소 생성
  **ELEMENTS** 지시어는 각 열 값이 XML의 요소로 매핑되는 XML을 구성합니다. 열 값이 NULL이면 요소가 추가되지 않습니다. ELEMENTS 지시어에 선택 항목인 **XSINIL** 매개 변수를 지정하면 NULL 값에 대해서도 요소가 생성되도록 요청할 수 있습니다. 이 경우 **xsi:nil** 특성이 TRUE로 설정된 요소가 각 NULL 열 값에 대해 반환됩니다.  
  
## 참고 항목  
 [FOR XML에서 RAW 모드 사용](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
  
  