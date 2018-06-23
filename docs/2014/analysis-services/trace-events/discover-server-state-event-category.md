---
title: Discover Server State 이벤트 범주 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Discover Server State event category
- server state events [Analysis Services]
- discover server state events
- event classes [Analysis Services], discover server state
ms.assetid: b62ebf66-d090-4f74-8c83-11ed518b2018
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 1e1ae268d3263fb672a8d0bda85b23774aca4ad2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36186153"
---
# <a name="discover-server-state-event-category"></a>Discover Server State 이벤트 범주
  Discover Server State 이벤트 범주에는 다음 표에 설명된 이벤트 클래스가 있습니다.  
  
|Event Class|이벤트 ID|Description|  
|-----------------|--------------|-----------------|  
|Server State Discover Begin|33|추적이 시작된 이후의 서버 상태 XMLA 검색 시작 이벤트를 모두 수집합니다.|  
|Server State Discover Data|34|추적이 시작된 이후의 서버 상태 XMLA 검색 데이터 이벤트를 모두 수집합니다. 이러한 이벤트는 검색 요청에 대한 응답의 내용을 캡처합니다.|  
|Server State Discover End|35|추적이 시작된 이후의 서버 상태 XMLA 검색 종료 이벤트를 모두 수집합니다.|  
  
 각각의 Query Events 이벤트 클래스와 연관된 열에 대한 자세한 내용은 [Discover Server State Events Data Columns](discover-server-state-events-data-columns.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 추적 이벤트](analysis-services-trace-events.md)  
  
  