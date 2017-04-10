---
title: "DTAInput 요소(DTA) | Microsoft Docs"
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
  - "DTAInput 요소"
ms.assetid: 40c19abf-ded5-43de-be96-5b43b1b81b03
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# DTAInput 요소(DTA)
  데이터베이스 엔진 튜닝 관리자에 대한 XML 입력의 정의를 포함합니다.  
  
## 구문  
  
```  
  
<DTAXML>  
    <DTAInput>  
    ...code removed here...  
    </DTAInput>  
```  
  
## 요소 특징  
  
|특징|설명|  
|---------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|**DTAXML** 요소마다 한 번만 지정할 수 있습니다(옵션).|  
  
## 요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[DTAXML 요소&#40;DTA&#41;](../../tools/dta/dtaxml-element-dta.md)|  
|**자식 요소**|[Server 요소&#40;DTA&#41;](../../tools/dta/server-element-dta.md)<br /><br /> [Workload 요소&#40;DTA&#41;](../../tools/dta/workload-element-dta.md)<br /><br /> [TuningOptions 요소&#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)<br /><br /> [Configuration 요소&#40;DTA&#41;](../../tools/dta/configuration-element-dta.md)|  
  
## 주의  
 이 요소는 데이터베이스 엔진 튜닝 관리자 입력 스키마 계층의 루트입니다. 데이터베이스 엔진 튜닝 관리자에 대한 입력은 튜닝할 데이터베이스가 있는 서버, 작업, 튜닝 옵션 또는 사용자 지정 구성을 지정하는 인수가 될 수 있습니다.  
  
## 예제  
 **DTAInput** 요소의 사용 예를 보려면 [단순 XML 입력 파일 샘플&#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md)을 참조하세요.  
  
## 참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  