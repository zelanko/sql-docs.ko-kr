---
title: "Partitioning 요소(DTA) | Microsoft Docs"
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
  - "Partitioning 요소"
ms.assetid: 9bc5d1d5-27a7-4434-966f-c3935794af27
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# Partitioning 요소(DTA)
  분석 도중에 데이터베이스 엔진 튜닝 관리자에서 사용하도록 파티션 구성표를 포함합니다.  
  
## 구문  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <Partitioning>...</Partitioning>  
```  
  
## 요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string**, 최대 길이 없음|  
|**허용된 값**|**NONE**<br /> 분할 안 함<br /><br /> **FULL**<br /> 전체 분할 (성능 향상 중심)<br /><br /> **ALIGNED**<br /> 정렬된 분할만 (관리 효율성 중심)<br /><br /> 이 요소에 이러한 값 중 하나만 사용합니다.<br /><br /> **ALIGNED** 는 데이터베이스 엔진 튜닝 관리자가 생성한 권장 구성에서 모든 제안된 인덱스는 인덱스가 정의된 기본 테이블과 동일한 방식으로 분할된다는 것을 의미합니다. 인덱싱된 뷰의 비클러스터형 인덱스는 인덱싱된 뷰에 정렬됩니다.|  
|**기본값**|**NONE**|  
|**발생 빈도**|**TuningOptions** 요소를 사용하지 않을 경우 **DropOnlyMode** 요소에 한 번만 지정해야 합니다. **DropOnlyMode** 를 사용하는 경우 **Partitioning**는 사용할 수 없습니다. 이러한 요소는 함께 사용할 수 없습니다.|  
  
## 요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[TuningOptions 요소&#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**자식 요소**|없음|  
  
## 예제  
 이 요소의 사용 예제를 보려면 [단순 XML 입력 파일 예제&#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)를 참조하세요.  
  
## 참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  