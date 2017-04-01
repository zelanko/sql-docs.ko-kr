---
title: "Create 요소(DTA) | Microsoft Docs"
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
  - "Create 요소(DTA)"
ms.assetid: 9d076c90-f933-45f4-b6d9-447793f6528b
caps.latest.revision: 12
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 12
---
# Create 요소(DTA)
  인덱스, 통계 또는 힙 구조에 대한 정보를 사용자 지정 구성에 포함합니다.  
  
## 구문  
  
```  
  
<Recommendation>  
    <Create>  
    ...code removed here...  
    </Create>  
</Recommendation>  
```  
  
## 요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|각 물리적 디자인 구조 유형(인덱스, 통계 또는 힙 구조)에 한 번만 지정해야 합니다.|  
  
## 요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Recommendation 요소&#40;DTA&#41;](../../tools/dta/recommendation-element-dta.md)|  
|**자식 요소**|[Index 요소&#40;DTA&#41;](../../tools/dta/index-element-dta.md)<br /><br /> **Statistics** 요소(자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://schemas.microsoft.com/sqlserver/) 참조)<br /><br /> **Heap** 요소(자세한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://schemas.microsoft.com/sqlserver/) 참조)|  
  
## 주의  
 데이터베이스 엔진 튜닝 관리자 XML 스키마에서 이 요소의 이름은 **CreateTypecomplexType**입니다. 이 요소는 사용자 지정 구성에 대한 인덱스, 통계 및 힙 구조를 만드는 데 사용됩니다. 이 **Create** 요소를 뷰(**CreateViewType**) 또는 분할(**CreatePType**)을 만드는 데 사용할 수 있는 다른 유형과 혼동하지 마세요. 이러한 기타 **Create** 요소 유형에 대한 내용은 [데이터베이스 엔진 튜닝 관리자 XML 스키마](http://schemas.microsoft.com/sqlserver/)를 참조하세요.  
  
## 예제  
 이 요소의 사용 예를 보려면 [사용자 정의 구성이 포함된 XML 입력 파일 샘플&#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md)를 참조하세요.  
  
## 참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  