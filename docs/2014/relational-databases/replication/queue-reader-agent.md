---
title: 큐 판독기 에이전트 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.monitor.queuereaderagent.f1
helpviewer_keywords:
- Queue Reader Agent dialog box
ms.assetid: f02d24b6-dcb5-4126-b56e-fab41cfe4337
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 401d36c399c88088475a989a355a9430ce6e3818
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52777945"
---
# <a name="queue-reader-agent"></a>큐 판독기 에이전트
  **큐 판독기 에이전트** 대화 상자에서는 상태, 기록, 정보 메시지 및 모든 오류 메시지를 포함한 큐 판독기 에이전트에 대한 자세한 정보를 표시합니다.  
  
## <a name="options"></a>변수  
 **보기** 메뉴에서 보려는 큐 판독기 에이전트 세션을 선택한 다음 **큐 판독기 에이전트의 세션**표에서 특정 세션을 선택합니다. **선택한 세션의 동작**표에 이 세션에 대한 자세한 정보가 표시됩니다. 선택한 세션이 오류로 인해 종료될 경우 **선택한 세션에 대한 오류 정보 또는 메시지** 라는 텍스트 영역 또한 표시됩니다.  
  
 **보기**  
 확인할 큐 판독기 에이전트 세션을 선택합니다. 큐 판독기 에이전트는 일반적으로 계속 실행되므로 하나의 세션만 표시될 수 있습니다.  
  
 **상태**  
 큐 판독기 에이전트의 상태입니다. 다음 목록에서는 가능한 상태 값을 보여 줍니다.  
  
-   Error  
  
-   실패한 명령 다시 시도 중  
  
-   실행 중이 아님  
  
-   실행 중  
  
 **Start Time**  
 세션의 시작 시간입니다.  
  
 **종료 시간**  
 세션의 종료 시간입니다. 에이전트가 중지되지 않은 경우 이 필드는 비어 있습니다.  
  
 **기간**  
 이 세션에서 큐 판독기 에이전트가 실행된 시간입니다. 에이전트가 현재 실행되고 있는 경우 이 시간은 경과된 시간을 나타내고 에이전트 세션이 종료된 경우에는 총 세션 시간을 나타냅니다.  
  
 **오류 메시지**  
 세션이 오류로 인해 종료된 경우 이 필드는 큐 판독기 에이전트가 기록한 마지막 오류 메시지를 표시합니다. 세션이 오류 없이 종료된 경우에는 필드가 비어 있습니다.  
  
 **동작 메시지**  
 선택한 세션 중에 큐 판독기 에이전트가 기록한 모든 정보 메시지 및 오류 메시지입니다.  
  
 **동작 시간**  
 **동작 메시지** 열에서 설명한 동작이 수행된 시간입니다.  
  
 **선택한 세션에 대한 오류 정보 또는 메시지**  
 선택한 세션의 **상태** 열에 **오류** 값이 표시되는 경우에만 표시됩니다. 이 텍스트 영역은 오류 발생 시 시도한 명령과 자세한 오류 정보를 표시합니다. 오류와 관련된 추가 내용으로 연결되는 링크도 포함되어 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 모니터 시작](monitor/start-the-replication-monitor.md)   
 [게시 관련 에이전트에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](monitor/view-information-and-perform-tasks-for-publication-agents.md)   
 [복제 모니터링](monitoring-replication.md)   
 [복제 에이전트 개요](agents/replication-agents-overview.md)  
  
  
