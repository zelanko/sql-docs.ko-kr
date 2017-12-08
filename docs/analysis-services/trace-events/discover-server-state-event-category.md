---
title: "Discover Server State 이벤트 범주 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: trace-events
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Discover Server State event category
- server state events [Analysis Services]
- discover server state events
- event classes [Analysis Services], discover server state
ms.assetid: b62ebf66-d090-4f74-8c83-11ed518b2018
caps.latest.revision: "25"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f553fc692cb15d5393718c3b40d2c5d33dbcf222
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="discover-server-state-event-category"></a>Discover Server State 이벤트 범주
  Discover Server State 이벤트 범주에는 다음 표에 설명된 이벤트 클래스가 있습니다.  
  
|Event Class|이벤트 ID|Description|  
|-----------------|--------------|-----------------|  
|Server State Discover Begin|33|추적이 시작된 이후의 서버 상태 XMLA 검색 시작 이벤트를 모두 수집합니다.|  
|Server State Discover Data|34|추적이 시작된 이후의 서버 상태 XMLA 검색 데이터 이벤트를 모두 수집합니다. 이러한 이벤트는 검색 요청에 대한 응답의 내용을 캡처합니다.|  
|Server State Discover End|35|추적이 시작된 이후의 서버 상태 XMLA 검색 종료 이벤트를 모두 수집합니다.|  
  
 각각의 Query Events 이벤트 클래스와 연관된 열에 대한 자세한 내용은 [Discover Server State Events Data Columns](../../analysis-services/trace-events/discover-server-state-events-data-columns.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 추적 이벤트](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
