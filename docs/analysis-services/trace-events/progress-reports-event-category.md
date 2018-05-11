---
title: Progress Reports 이벤트 범주 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: trace-events
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d4722ea18e493a243e6adaf64555c4e90ec4b165
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="progress-reports-event-category"></a>Progress Reports 이벤트 범주
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Progress Reports 이벤트 범주에는 다음 표에 설명된 이벤트 클래스가 있습니다.  
  
|Event Class|이벤트 ID|Description|  
|-----------------|--------------|-----------------|  
|Progress Report Begin|5|추적이 시작된 이후의 진행률 보고서 시작 이벤트를 모두 수집합니다.|  
|Progress Report End|6|추적이 시작된 이후의 진행률 보고서 종료 이벤트를 모두 수집합니다.|  
|Progress Report Current|7|추적이 시작된 이후의 진행률 보고서 현재 이벤트를 모두 수집합니다. 예를 들어 처리가 진행되는 동안 현재 보고서에는 차원, 파티션, 큐브 등의 처리 중인 개체에 대한 처리 정보가 포함됩니다.|  
|Progress Report Error|8|추적이 시작된 이후의 진행률 보고서 오류 이벤트를 모두 수집합니다.|  
  
 각각의 Progress Report Begin 이벤트는 진행률 이벤트 스트림으로 시작되어 Progress Report End 이벤트로 종료됩니다. 이 스트림에는 Progress Report Current 이벤트와 Progress Report Error 이벤트가 개수에 관계없이 포함될 수 있습니다.  
  
 각각의 Progress Reports 이벤트 클래스와 연관된 열에 대한 자세한 내용은 [Progress Reports Data Columns](../../analysis-services/trace-events/progress-reports-data-columns.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 추적 이벤트](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  
