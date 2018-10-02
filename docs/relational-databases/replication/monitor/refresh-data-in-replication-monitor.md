---
title: 복제 모니터에서 데이터 새로 고침 | Microsoft 문서
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- refreshing data
ms.assetid: e9582244-7d00-45f4-be16-020a65c76a5e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f772f42cc4afd6d187f4d53b0077f4417009f180
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855931"
---
# <a name="refresh-data-in-replication-monitor"></a>복제 모니터에서 데이터 새로 고침
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  복제 모니터에서는 주 창 및 세부 정보 창(주 창에서 시작되는 창)을 자동으로 또는 수동으로 새로 고칠 수 있습니다. 창을 수동으로 새로 고치려면 F5 키를 누르면 됩니다. 기본적으로 주 창은 5분마다 자동으로 새로 고쳐집니다. 이러한 새로 고침 빈도는 게시자별로 사용자 지정할 수 있습니다.  
  
 복제 모니터에 표시된 데이터는 캐시에서 쿼리됩니다. 캐시와 복제 모니터 새로 고침의 관계에 대한 자세한 내용은 [캐싱, 새로 고침 및 복제 모니터 성능](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md)을 참조하세요. 복제 모니터를 시작하는 방법은 [복제 모니터 시작](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)을 참조하세요.  
  
### <a name="to-set-refresh-options-for-replication-monitor"></a>복제 모니터에 대한 새로 고침 옵션을 설정하려면  
  
1.  복제 모니터의 왼쪽 창에서 게시자를 마우스 오른쪽 단추로 클릭한 다음 **게시자 설정**을 클릭합니다.  
  
2.  **게시자 설정** 대화 상자에서 **자동 새로 고침** 및 **새로 고침 빈도** 옵션을 설정합니다. **자동 새로 고침** 설정은 복제 모니터의 주 창에 영향을 줍니다. **새로 고침 빈도** 설정은 자동으로 새로 고치도록 설정된 세부 정보 창에도 영향을 줍니다. 이러한 설정을 변경하면 변경 후 열린 세부 정보 창에만 영향을 줍니다.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-specify-that-a-detail-window-should-automatically-refresh"></a>세부 정보 창이 자동으로 새로 고쳐지도록 지정하려면  
  
1.  다음과 같이 예를 들어 다음과 같이 사용할 수 있습니다.  
  
    1.  왼쪽 창에서 게시자 그룹을 확장하고 해당 게시자를 확장한 다음 해당 게시를 클릭합니다.  
  
    2.  **모든 구독** 탭을 클릭합니다.  
  
    3.  구독을 마우스 오른쪽 단추로 클릭한 다음 **자세히 보기**를 클릭합니다.  
  
2.  **구독 \<SubscriptionName>** 세부 정보 창에서 **작업**을 클릭한 다음 **자동 새로 고침**을 클릭합니다. 새로 고침 빈도는 **게시자 설정** 대화 상자의 **새로 고침 빈도** 설정에 의해 결정됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터링](../../../relational-databases/replication/monitor/monitoring-replication-overview.md)  
  
  
