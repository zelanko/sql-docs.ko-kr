---
title: "Progress Reports 이벤트 범주 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- progress events [Analysis Services]
- Progress Reports event category
- event classes [Analysis Services], progress reports
ms.assetid: c130f160-28ef-49bc-9ee6-da47dc9aab2a
caps.latest.revision: 23
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3489d5176553ba8482646610a048955b93399043
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

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
  
 각각의 Progress Reports 이벤트 클래스와 연관된 열에 대한 자세한 내용은 [Progress Reports Data Columns](../../analysis-services/trace-events/progress-reports-data-columns.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 추적 이벤트](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  

