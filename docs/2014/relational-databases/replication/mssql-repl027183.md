---
title: MSSQL_REPL027183 | Microsoft 문서
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL027183 error
ms.assetid: 52c271ac-1a0e-43d5-85d4-35886d1efd32
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 87adf79d9420f70e132fd9a6c41a9ddacf298fa7
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52776975"
---
# <a name="mssqlrepl027183"></a>MSSQL_REPL027183
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|27183|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|병합 프로세스에서 매개 변수가 있는 행 필터를 사용하여 아티클의 변경 내용을 열거하지 못했습니다. 이 오류가 계속되면 이 프로세스에 대한 쿼리 제한 시간을 늘리고 게시 보존 기간을 줄인 다음 게시된 테이블의 인덱스를 향상시키십시오.|  
  
## <a name="explanation"></a>설명  
 이 오류는 필터링된 게시에서 변경 내용을 처리하는 동안 병합 에이전트 제한 시간에 도달한 경우 발생합니다. 다음 문제 중 하나로 인해 제한 시간에 도달했을 수 있습니다.  
  
-   사전 계산 파티션 최적화를 사용하지 않았습니다.  
  
-   열의 인덱스 조각화가 필터링에 사용되었습니다.  
  
-   **MSmerge_tombstone**, **MSmerge_contents**, **MSmerge_genhistory**와 같은 큰 병합 메타데이터 테이블이 있습니다.  
  
-   필터링된 테이블이 고유 키에 조인되어 있지 않고 많은 테이블이 조인 필터와 관련되어 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
 이 문제를 해결하려면  
  
-   오류를 일으킨 기본 문제를 해결하는 동안 병합 에이전트에서 계속 처리 작업을 수행하려면 **-QueryTimeOut** 매개 변수의 값을 늘립니다. 에이전트 프로필 및 명령줄에서 에이전트 매개 변수를 지정할 수 있습니다. 참조 항목:  
  
    -   [복제 에이전트 프로필 작업](agents/replication-agent-profiles.md)  
  
    -   [복제 에이전트의 명령 프롬프트 매개 변수 보기 및 수정&#40;SQL Server Management Studio&#41;](agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [복제 에이전트 실행 파일 개념](concepts/replication-agent-executables-concepts.md)  
  
-   사전 계산 파티션 최적화를 사용합니다(가능한 경우). 많은 게시 요구 사항이 충족되면 이 최적화가 기본적으로 사용됩니다. 이러한 요구 사항에 대한 자세한 내용은 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](merge/parameterized-filters-optimize-for-precomputed-partitions.md)를 참조하세요. 게시가 이러한 요구 사항을 충족하지 않는 경우 게시를 다시 디자인하십시오.  
  
-   복제는 보존 기간에 도달할 때까지 게시 및 구독 데이터베이스의 메타데이터를 정리할 수 없으므로 게시 보존 기간에 대해 가능한 가장 낮은 설정을 지정합니다. 자세한 내용은 [Subscription Expiration and Deactivation](subscription-expiration-and-deactivation.md)을 참조하세요.  
  
-   병합 복제 유지 관리의 한 부분으로 병합 복제와 연결된 **MSmerge_contents**, **MSmerge_genhistory**, 및 **MSmerge_tombstone**하십시오 **MSmerge_current_partition_mappings**, 및 **MSmerge_ past_partition_mappings**합니다. 이러한 테이블의 인덱스를 주기적으로 다시 만듭니다. 자세한 내용은 [인덱스 다시 구성 및 다시 작성](../indexes/indexes.md)을 참조하세요.  
  
-   필터링에 사용된 열이 올바로 인덱싱되는지 확인하고 이러한 인덱스를 다시 작성합니다(필요한 경우). 자세한 내용은 [인덱스 다시 구성 및 다시 작성](../indexes/indexes.md)을 참조하세요.  
  
-   고유 열을 기반으로 하는 조인 필터에 대해 **join_unique_key** 속성을 설정합니다. 자세한 내용은 [Join Filters](merge/join-filters.md)을(를) 참조하세요.  
  
-   조인 필터 계층에서 테이블의 수를 제한합니다. 5개 이상의 테이블을 가진 조인 필터를 생성하는 경우 다른 해결책을 고려하는 것이 좋습니다. 크기가 작거나, 변경될 가능성이 없거나, 기본적으로 조회 테이블에 해당하는 테이블은 필터링하지 마십시오. 구독 간에 분할해야 하는 테이블 사이에서만 조인 필터를 사용합니다.  
  
-   동기화 사이에 있는 필터링된 테이블에 대한 변경 횟수를 줄이거나 병합 에이전트를 더 자주 실행합니다. 동기화 일정 설정 방법은 [Specify Synchronization Schedules](specify-synchronization-schedules.md)을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](errors-and-events-reference-replication.md)  
  
  
