---
title: "FeatureSet 요소(DTA) | Microsoft Docs"
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
  - "FeatureSet 요소"
ms.assetid: f2070c53-4a5c-4c11-ac38-96ee200c84f0
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# FeatureSet 요소(DTA)
  데이터베이스 엔진 튜닝 관리자에서 분석 도중에 사용하도록 할 물리적 디자인 구조(인덱스 또는 인덱싱된 뷰)를 포함합니다.  
  
## 구문  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <FeatureSet>...</FeatureSet>  
```  
  
## 요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string**, 최대 길이 없음|  
|**허용된 값**|**IDX_IV**<br /> 인덱스와 인덱싱된 뷰<br /><br /> **IDX**<br /> 인덱스만<br /><br /> **IV**<br /> 인덱싱된 뷰만<br /><br /> **NCL_IDX**<br /> 비클러스터형 인덱스만<br /><br /> 이 요소에 이러한 값 중 하나를 사용합니다.|  
|**기본값**|**IDX**|  
|**발생 빈도**|**TuningOptions** 요소가 사용되지 않을 경우 각 **DropOnlyMode** 요소에 한 번만 지정해야 합니다. **DropOnlyMode** 를 사용하는 경우 **FeatureSet**는 사용할 수 없습니다. 이러한 요소는 함께 사용할 수 없습니다.|  
  
## 요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[TuningOptions 요소&#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**자식 요소**|없음|  
  
## 예제  
 이 요소의 사용 예제를 보려면 [단순 XML 입력 파일 예제&#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)를 참조하세요.  
  
## 참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  