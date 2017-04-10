---
title: "Index의 Filegroup 요소(DTA) | Microsoft Docs"
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
  - "Filegroup 요소 [DTA]"
ms.assetid: 7078d2fb-fa77-44fc-beb3-c095088fcb85
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# Index의 Filegroup 요소(DTA)
  사용자 지정 구성에서 인덱스를 만들려는 파일 그룹을 지정합니다.  
  
## 구문  
  
```  
  
<Index>  
  <Name>...</Name>  
  <Column>  
    <Name>...</Name>  
  <Filegroup>...</Filegroup>  
```  
  
## 요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string**, 길이 제한 없음|  
|**기본값**|없음|  
|**발생 빈도**|(선택 사항) 각 **Index** 요소에 한 번만 사용할 수 있습니다. **PartitionScheme** 및 **PartitionColumn** 요소를 **Index** 요소에 지정한 경우 이 옵션을 사용할 수 없습니다.|  
  
## 요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Index 요소&#40;DTA&#41;](../../tools/dta/index-element-dta.md)|  
|**자식 요소**|없음|  
  
## 예제  
 이 요소의 사용 예제를 보려면 [사용자 지정 구성이 포함된 XML 입력 파일 예제&#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)를 참조하세요.  
  
## 참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  