---
title: "Server의 Name 요소(DTA) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "XML"
helpviewer_keywords: 
  - "Name 요소"
ms.assetid: 4c94754d-6d62-4357-8ce7-f107ebf90c71
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# Server의 Name 요소(DTA)
  튜닝할 데이터베이스가 상주하는 서버의 이름을 포함합니다.  
  
## 구문  
  
```  
  
...code removed here...  
<Server>  
    <Name>...</Name>  
```  
  
## 요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string**, 1에서 255자 사이|  
|**기본값**|없음|  
|**발생 빈도**|**Server** 요소마다 한 번만 지정해야 함|  
  
## 요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Server 요소&#40;DTA&#41;](../../tools/dta/server-element-dta.md)|  
|**자식 요소**|없음|  
  
## 예제  
 이 **Name** 요소의 사용 예는 [서버 요소&#40;DTA&#41;](../../tools/dta/server-element-dta.md)를 참조하세요.  
  
## 참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  