---
title: "EventString 요소 (DTA) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: EventString element
ms.assetid: f76c37b4-2f6e-4274-8ee2-87e89d98e8a2
caps.latest.revision: "12"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e76b650d9f7cf59d58cc32ff124c41091c64fbc2
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="eventstring-element-dta"></a>EventString 요소(DTA)
  XML 입력 파일에서 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 작업을 직접 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Workload>  
    <EventString Weight="...">  
    ...code removed here...  
    </EventString>  
</Workload>  
```  
  
## <a name="element-attributes"></a>요소 특성  
  
|Attribute|설명|  
|---------------|-----------------|  
|**Weight**|(선택 사항) 지정한 이벤트에 대한 쿼리 가중치 요인(중요도 요인)을 지정합니다. **float** 데이터 형식을 사용하여 가중치를 지정할 수 있습니다(예: **Weight**="100.01"). **Weight** 에 지정할 수 있는 최소값은 "0"입니다.|  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string**, 길이 제한 없음|  
|**기본값**|없음|  
|**발생 빈도**|다른 작업 유형이 지정되지 않은 경우 한 번만 지정해야 합니다. **EventString**부모에 대해 **File**, **Database** 또는 **Workload** 자식 요소를 지정해야 하지만 한 유형만 사용할 수 있습니다. 예를 들어 **EventString** 요소로 작업을 지정할 경우 동일한 XML 입력 파일에서 **File** 요소로 작업을 지정할 수 없습니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[Workload 요소&#40;DTA&#41;](../../tools/dta/workload-element-dta.md)|  
|**자식 요소**|없음|  
  
## <a name="example"></a>예제  
 이 요소의 사용 예를 보려면 [인라인 워크로드가 포함된 XML 입력 파일 샘플&#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
