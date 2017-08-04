---
title: "DatabaseToConnect 요소 (DTA) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 94746d3007587223ba1b2ae6a3868ce3a013bafd
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# DatabaseToConnect 요소(DTA)
  작업 튜닝 시 데이터베이스 엔진 튜닝 관리자가 연결되는 첫 번째 데이터베이스를 지정합니다.  
  
## 구문  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## 요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string**, 길이 제한 없음|  
|**기본값**|없음|  
|**발생 빈도**|(선택 사항) 각 **TuningOptions** 요소에 한 번만 사용할 수 있습니다.|  
  
## 요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[TuningOptions 요소 &#40; DTA &#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**자식 요소**|없음|  
  
## 주의  
 **DatabaseToConnect** 를 사용하여 데이터베이스 엔진 튜닝 관리자가 튜닝 세션을 시작할 때 연결되는 첫 번째 데이터베이스의 이름을 지정할 수 있습니다. 이 요소에서는 데이터베이스를 하나만 지정할 수 있습니다. 여러 데이터베이스 이름을 지정할 경우 데이터베이스 엔진 튜닝 관리자는 오류를 반환합니다.  
  
## 예제  
 사용 예제를 보려면 [인라인 워크로드가 포함된 XML 입력 파일 예제&#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md)를 참조하세요.  
  
## 관련 항목:  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
