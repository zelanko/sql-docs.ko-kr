---
title: MSSQL_ENG014160 | Microsoft 문서
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014160 error
ms.assetid: d0f3855e-d095-4a81-a5bd-9d7ad51f2c77
caps.latest.revision: 11
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b1f8d07df99b226597b0dbcd683e2a87368ad3cb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="mssqleng014160"></a>MSSQL_ENG014160
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|14160|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|게시 [%s]에 대한 임계값 [%s:%s]이(가) 설정되어 있습니다. 병합 에이전트가 실행 중이고 필요한 요구 사항에 맞는지 확인하십시오. 이 게시에 대해 하나 이상의 구독이 만료되었습니다.|  
  
## <a name="explanation"></a>설명  
 복제를 통해 임박한 구독 만료 등의 여러 조건에 대한 경고를 설정할 수 있습니다. 지정된 *보존 기간*내에 동기화되지 않는 구독을 만료할 수 있습니다. 자세한 내용은 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)를 참조하세요.  
  
 복제 모니터 또는 [sp_replmonitorchangepublicationthreshold](../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md)를 사용하여 경고를 설정할 경우 경고가 트리거되는 시기를 결정하는 임계값을 지정하십시오. 임계값에 도달하거나 임계값이 초과되면 복제 모니터에 경고가 표시되며 Windows 이벤트 로그에 이벤트가 기록됩니다. 또한 임계값에 도달하면 SQL Server 에이전트 경고가 트리거됩니다. 자세한 내용은 [복제 모니터에 임계값 및 경고 설정](../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md) 및 [프로그래밍 방식으로 복제 모니터링](../../relational-databases/replication/monitor/programmatically-monitor-replication.md)을 참조하세요.  
  
## <a name="user-action"></a>사용자 동작  
 이 문제의 해결 방법은 경고 발생 원인에 따라 다릅니다.  
  
-   임계값을 초과했지만 구독이 아직 만료되지 않은 경우 구독을 동기화하십시오. 자세한 내용은 [데이터 동기화](../../relational-databases/replication/synchronize-data.md)를 참조하세요.  
  
-   에이전트가 실행 중이지만 변경 내용을 제대로 복제하지 않으면 구독이 만료될 수 있습니다. 트랜잭션 복제의 경우 배포 에이전트와 로그 판독기 에이전트가 실행 중인지 확인하십시오. 병합 복제의 경우 병합 에이전트가 실행 중인지 확인하십시오. 이러한 에이전트를 시작하는 방법에 대한 자세한 내용은 [복제 에이전트 시작 및 중지&#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 및 [복제 에이전트 실행 파일 개념](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)을 참조하세요.  
  
-   구독이 만료된 경우 해당 구독은 구독 유형 및 만료된 기간에 따라 다시 초기화되거나 삭제 후 다시 생성되어야 합니다. 자세한 내용은 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [오류 및 이벤트 참조&#40;복제&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
