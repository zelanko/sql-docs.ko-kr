---
title: SQL Server, Broker Activation 개체 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Broker Activation
- Broker Activation object
ms.assetid: cd9b6880-c924-42c7-b333-09c303317c0b
caps.latest.revision: 19
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4de21798991eb269cdca7232eb38ecdacc93e956
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37320353"
---
# <a name="sql-server-broker-activation-object"></a>SQL Server, Broker 활성화 개체
  **SQLServer:BrokerActivation** 성능 개체에는 저장 프로시저 활성화에 대한 정보를 보고하는 성능 카운터가 포함되어 있습니다. 다음 표에서는 이 개체가 포함하는 카운터를 나열합니다.  
  
|SQL Server, Broker 활성화 카운터|Description|  
|-------------------------------------------|-----------------|  
|**Stored Procedures Invoked/sec**|이 카운터는 인스턴스의 모든 큐 모니터에서 호출하는 초당 총 활성화 저장 프로시저 수를 보고합니다.|  
|**Task Limit Reached**|이 카운터는 큐 모니터가 새 태스크를 시작했지만 해당 큐에 대한 최대 수의 작업이 이미 실행 중이기 때문에 시작하지 못한 총 횟수를 보고합니다.|  
|**Task Limit Reached/sec**|이 카운터는 큐 모니터가 새 태스크를 시작했지만 해당 큐에 대한 최대 수의 작업이 이미 실행 중이기 때문에 시작하지 못한 초당 횟수를 보고합니다.|  
|**Tasks Aborted/sec**|이 카운터는 오류로 인해 종료되거나 메시지를 받는 데 실패하여 큐 모니터에서 중단시킨 활성화 저장 프로시저 태스크 수를 보고합니다.|  
|**Tasks Running**|이 카운터는 현재 실행 중인 활성화 저장 프로시저 수를 보고합니다.|  
|**Tasks Started/sec**|이 카운터는 인스턴스의 모든 큐 모니터에서 시작하는 초당 활성화 저장 프로시저 수를 보고합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [sys.dm_broker_activated_tasks&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-broker-activated-tasks-transact-sql)   
 [sys.dm_broker_queue_monitors&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-broker-queue-monitors-transact-sql)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)  
  
  
