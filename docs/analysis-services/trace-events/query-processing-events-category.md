---
title: "쿼리 이벤트 범주를 처리 합니다. | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: a94b3198-be85-4935-845d-1cd4e121fc94
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d547a887a05120405f6bf26049a567e1aa8026c8
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="query-processing-events-category"></a>Query Processing 이벤트 범주
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
Query Processing 이벤트 범주에는 다음 표에 설명된 이벤트 클래스가 있습니다.  
  
|**Event Class**|**이벤트 ID**|**Description**|  
|---------------------|------------------|---------------------|  
|Query Subcube|11|사용 빈도 기반 최적화에 대한 쿼리 하위 큐브입니다.|  
|Query Subcube Verbose|12|세부 정보가 포함된 쿼리 하위 큐브입니다. 이 이벤트를 설정하면 성능이 저하될 수 있습니다.|  
|Get Data From Aggregation|60|집계 데이터를 가져와 쿼리에 응답합니다. 이 이벤트를 설정하면 성능이 저하될 수 있습니다.|  
|Get Data From Cache|61|캐시 중 하나의 데이터를 가져와 쿼리에 응답합니다. 이 이벤트를 설정하면 성능이 저하될 수 있습니다.|  
|Query Cube Begin|70|추적이 시작된 이후의 모든 Query Cube Begin 이벤트를 수집합니다.|  
|Query Cube End|71|추적이 시작된 이후의 모든 Query Cube End 이벤트를 수집합니다.|  
|Calculate Non Empty Begin|72|비어 있지 않음 계산을 시작합니다.|  
|Calculate Non Empty Current|73|비어 있지 않음 계산을 현재 실행 중입니다.|  
|Calculate Non Empty End|74|비어 있지 않음 계산을 종료합니다.|  
|Serialize Results Begin|75|결과 직렬화를 시작합니다.|  
|Serialize Results Current|76|결과 직렬화를 현재 실행 중입니다.|  
|Serialize Results End|77|결과 직렬화를 종료합니다.|  
|Execute MDX Script Begin|78|MDX 스크립트 실행을 시작합니다.|  
|Execute MDX Script Current|79|MDX 스크립트를 현재 실행 중입니다.|  
|Execute MDX Script End|80|MDX 스크립트 실행을 종료합니다.|  
|Query Dimension|81|쿼리 차원입니다.|  
|VertiPaq SE Query Begin|82|VertiPaq SE 쿼리|  
|VertiPaq SE Query End|83|VertiPaq SE 쿼리|  
  
 각각의 Query Processing 이벤트 클래스와 연관된 열에 대한 자세한 내용은 [Query Processing Events Data Columns](../../analysis-services/trace-events/query-processing-events-data-columns.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 추적 이벤트](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
