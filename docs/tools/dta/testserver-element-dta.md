---
title: TestServer 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: dta
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- TestServer element
ms.assetid: caa3547a-2cd5-47ad-ace2-a36752835cfe
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 70efce8b1aede11f3892b6c20c06fa6d1c143a43
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="testserver-element-dta"></a>TestServer 요소(DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 프로덕션 서버를 튜닝할 때 사용할 테스트 서버를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<TuningOptions>  
  <TestServer>...</TestServer>  
   ...code removed here...  
</TuningOptions>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string**, 길이 제한 없음|  
|**기본값**|없음|  
|**발생 빈도**|(선택 사항) 각 **TuningOptions** 요소에 한 번만 사용할 수 있습니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[TuningOptions 요소&#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**자식 요소**|없음|  
  
## <a name="example"></a>예제  
 이 요소의 사용 예제를 보려면 [프로덕션 서버 튜닝 로드 줄이기](../../relational-databases/performance/reduce-the-production-server-tuning-load.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
