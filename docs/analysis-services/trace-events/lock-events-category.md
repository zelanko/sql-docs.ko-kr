---
title: "잠금 이벤트 범주 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: trace-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 06427f8e-89bb-4710-a0c1-dc5e42b7e95e
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4fbe7cccb4caaa0b87a7f502ed3ca714e3efa515
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="lock-events-category"></a>잠금 이벤트 범주
  Locks Events 이벤트 범주에는 다음 표에 설명된 이벤트 클래스가 있습니다.  
  
|Event Class|이벤트 ID|Description|  
|-----------------|--------------|-----------------|  
|Deadlock|50|추적이 시작된 이후의 모든 메타데이터 잠금 교착 상태 이벤트를 수집합니다.|  
|Lock timeout|51|추적이 시작된 이후의 모든 메타데이터 잠금 제한 시간 이벤트를 수집합니다.|  
|Lock Acquired|52|추적이 시작된 이후의 획득된 잠금에 대한 정보를 수집합니다.|  
|Lock Released|53|추적이 시작된 이후의 해제된 잠금에 대한 정보를 수집합니다.|  
|Lock Waiting|54|추적이 시작된 이후의 대기 상태에 있는 잠금에 대한 정보를 수집합니다.|  
  
 각각의 Lock 이벤트 클래스와 연관된 열에 대한 자세한 내용은 [Lock Events Data Columns](../../analysis-services/trace-events/lock-events-data-columns.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 추적 이벤트](../../analysis-services/trace-events/analysis-services-trace-events.md)  
  
  

