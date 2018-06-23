---
title: Progress Reports 이벤트 범주 | Microsoft Docs
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
- progress events [Analysis Services]
- Progress Reports event category
- event classes [Analysis Services], progress reports
ms.assetid: c130f160-28ef-49bc-9ee6-da47dc9aab2a
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8bcfa530f87d7a8caaee6814c2e2e2282e2783ed
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079363"
---
# <a name="progress-reports-event-category"></a>Progress Reports 이벤트 범주
  Progress Reports 이벤트 범주에는 다음 표에 설명된 이벤트 클래스가 있습니다.  
  
|Event Class|이벤트 ID|Description|  
|-----------------|--------------|-----------------|  
|Progress Report Begin|5|추적이 시작된 이후의 진행률 보고서 시작 이벤트를 모두 수집합니다.|  
|Progress Report End|6|추적이 시작된 이후의 진행률 보고서 종료 이벤트를 모두 수집합니다.|  
|Progress Report Current|7|추적이 시작된 이후의 진행률 보고서 현재 이벤트를 모두 수집합니다. 예를 들어 처리가 진행되는 동안 현재 보고서에는 차원, 파티션, 큐브 등의 처리 중인 개체에 대한 처리 정보가 포함됩니다.|  
|Progress Report Error|8|추적이 시작된 이후의 진행률 보고서 오류 이벤트를 모두 수집합니다.|  
  
 각각의 Progress Report Begin 이벤트는 진행률 이벤트 스트림으로 시작되어 Progress Report End 이벤트로 종료됩니다. 이 스트림에는 Progress Report Current 이벤트와 Progress Report Error 이벤트가 개수에 관계없이 포함될 수 있습니다.  
  
 각각의 Progress Reports 이벤트 클래스와 연관된 열에 대한 자세한 내용은 [Progress Reports Data Columns](progress-reports-data-columns.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 추적 이벤트](analysis-services-trace-events.md)  
  
  