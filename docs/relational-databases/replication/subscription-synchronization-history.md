---
title: "구독, 동기화 기록 | Microsoft 문서"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.rep.monitor.subscription.synchhistory.f1
ms.assetid: 85f666f6-14ee-4f19-b385-e5cc508aabe4
caps.latest.revision: "20"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ec6cfef6e74a1bf6479a78301f85c6d062992db3
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="subscription-synchronization-history"></a>구독, 동기화 기록
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)] **동기화 기록** 탭은 상태, 아티클 통계, 기록, 정보 메시지, 모든 오류 메시지 등 병합 에이전트에 대한 자세한 정보를 표시합니다.  
  
## <a name="options"></a>변수  
 **보기** 메뉴에서 보려는 병합 에이전트 세션을 선택한 다음 **병합 에이전트의 세션**표에서 특정 세션을 선택합니다. **선택한 세션에서 처리한 아티클**표에 이 세션에 대한 자세한 정보가 표시됩니다.  
  
 **보기**  
 확인할 병합 에이전트 세션을 선택합니다.  
  
 **상태**  
 세션 종료 시 병합 에이전트의 상태입니다. 다음 목록에서는 가능한 상태 값을 보여 줍니다.  
  
-   Error  
  
-   완료  
  
-   다시 시도 중  
  
-   실행 중  
  
 **Start Time**  
 세션의 시작 시간입니다.  
  
 **종료 시간**  
 세션의 종료 시간입니다. 에이전트가 중지되지 않은 경우 이 필드는 비어 있습니다.  
  
 **기간**  
 세션에서 병합 에이전트가 실행된 시간입니다. 에이전트가 현재 실행되고 있는 경우 이 시간은 경과된 시간을 나타내고 에이전트가 이전에 실행된 경우에는 총 시간을 나타냅니다.  
  
 **업로드된 명령**  
 병합 에이전트 세션 중 업로드된 행 수입니다.  
  
 **다운로드한 명령**  
 병합 에이전트 세션 중 다운로드된 행 수입니다.  
  
 **오류 메시지**  
 세션이 오류로 인해 종료된 경우 이 필드는 병합 에이전트에서 기록한 마지막 오류 메시지를 표시합니다. 세션이 오류 없이 종료된 경우에는 필드가 비어 있습니다.  
  
 **아티클**  
 게시에 있는 각 아티클의 이름입니다. 다음은 전체 게시의 처리 단계입니다.  
  
-   **초기화**. 병합 에이전트를 시작한다는 의미이며 스냅숏 적용과 관련된 구독 초기화와는 다릅니다.  
  
-   **스키마 변경 및 대량 삽입**  
  
-   **게시자에 변경 내용 업로드**  
  
-   **구독자에 변경 내용 다운로드**  
  
 선택한 세션에서 각 단계가 차지하는 시간 및 전체 시간 비율을 표에 표시할 수 있도록 단계를 포함합니다.  
  
 **총 %**  
 선택한 세션에서 각 단계가 차지하는 처리 시간 비율입니다.  
  
 **기간**  
 각 처리 단계에서 소요된 시간입니다. 병합 에이전트가 현재 세션에 대해 실행 중이면 이 시간은 경과된 시간을 나타내고 병합 에이전트가 이전에 실행된 경우에는 총 시간을 나타냅니다.  
  
 **Inserts**  
 선택한 세션의 이 단계에서 삽입된 행 수입니다.  
  
 **Updates**  
 선택한 세션의 이 단계에서 업데이트된 행 수입니다.  
  
 **Deletes**  
 선택한 세션의 이 단계에서 삭제된 행 수입니다.  
  
 **충돌**  
 선택한 세션의 충돌 수입니다.  
  
 **스키마 변경**  
 선택한 세션의 스키마 변경 수입니다. 구독 데이터베이스에서 스키마 변경 내용이 복제되고, 아티클이 추가 또는 삭제되고, 아티클 또는 구독 속성이 변경될 경우 스키마가 변경될 수 있습니다.  
  
 **선택한 세션에 대한 마지막 메시지**  
 이 텍스트 영역은 선택한 세션의 마지막 메시지를 표시합니다. 오류가 발생하면 오류 발생 시 시도한 명령과 자세한 오류 정보를 표시합니다. 오류와 관련된 추가 내용으로 연결되는 링크도 포함되어 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 모니터 시작](../../relational-databases/replication/monitor/start-the-replication-monitor.md)   
 [구독 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-subscription-agents.md)   
 [복제 모니터링](../../relational-databases/replication/monitor/monitoring-replication-overview.md)   
 [복제 에이전트 개요](../../relational-databases/replication/agents/replication-agents-overview.md)  
  
  
