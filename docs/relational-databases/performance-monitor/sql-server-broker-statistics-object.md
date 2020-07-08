---
title: SQL Server, Broker Statistics 개체 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Broker Statistics
- Broker Statistics object
ms.assetid: e9e36f01-93f6-4e6e-90c6-c7f3fd121737
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 6dd7b9d542bb72b570a59244639685d3e56d6377
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85657040"
---
# <a name="sql-server-broker-statistics-object"></a>SQL Server, Broker Statistics 개체
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  SQLServer:Broker Statistics 성능 개체는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 인스턴스에 대한 일반 [!INCLUDE[ssDE](../../includes/ssde-md.md)]정보를 보고하는 성능 카운터를 포함합니다. 다음 표에서는 이 개체가 포함하는 카운터를 나열합니다.  
  
|SQL Server Broker Statistics 카운터|Description|  
|-------------------------------------------|-----------------|  
|**Activation Errors Total**|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 활성화 저장 프로시저가 오류로 인해 종료된 횟수입니다.|  
|**Broker Transaction Rollbacks**|DML 문과 관련된 [!INCLUDE[ssSB](../../includes/sssb-md.md)](예: SEND 및 RECEIVE)를 포함하는 롤백된 트랜잭션의 수입니다.|  
|**Corrupted Messages Total**|인스턴스에 의해 수신된 손상된 메시지의 수입니다.|  
|**Dequeued Transmission Msgs/sec**|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 전송 큐에서 초당 제거된 메시지의 수입니다.|  
|**Dialog timer event count**|대화 프로토콜 계층에서 활성 상태인 타이머의 수입니다. 이 수는 활성 대화의 수에 해당됩니다.|  
|**Dropped Messages Total**|인스턴스에 의해 수신되었지만 큐에 배달할 수 없는 메시지의 수입니다.|  
|**Enqueued Local Messages Total**|인스턴스의 큐에 배치된 메시지의 수로 네트워크를 통해 도착하지 않은 메시지만 계산합니다.|  
|**Enqueued Local Messages/sec**|인스턴스의 큐에 배치된 초당 메시지의 수로 네트워크를 통해 도착하지 않은 메시지만 계산합니다.|  
|**Enqueued Messages Total**|인스턴스의 큐에 배치된 총 메시지 수입니다.|  
|**Enqueued Messages/sec**|인스턴스의 큐에 배치된 초당 메시지 수입니다. 여기에는 모든 우선 순위 수준의 메시지가 포함됩니다.|  
|**Enqueued P1 Msgs/sec**|인스턴스의 큐에 배치된 우선 순위가 1인 초당 메시지 조각의 수입니다.|  
|**Enqueued P2 Msgs/sec**|인스턴스의 큐에 배치된 우선 순위가 2인 초당 메시지 조각의 수입니다.|  
|**Enqueued P3 Msgs/sec**|인스턴스의 큐에 배치된 우선 순위가 3인 초당 메시지 조각의 수입니다.|  
|**Enqueued P4 Msgs/sec**|인스턴스의 큐에 배치된 우선 순위가 4인 초당 메시지 조각의 수입니다.|  
|**Enqueued P5 Msgs/sec**|인스턴스의 큐에 배치된 우선 순위가 5인 초당 메시지 조각의 수입니다.|  
|**Enqueued P6 Msgs/sec**|인스턴스의 큐에 배치된 우선 순위가 6인 초당 메시지 조각의 수입니다.|  
|**Enqueued P7 Msgs/sec**|인스턴스의 큐에 배치된 우선 순위가 7인 초당 메시지 조각의 수입니다.|  
|**Enqueued P8 Msgs/sec**|인스턴스의 큐에 배치된 우선 순위가 8인 초당 메시지 조각의 수입니다.|  
|**Enqueued P9 Msgs/sec**|인스턴스의 큐에 배치된 우선 순위가 9인 초당 메시지 조각의 수입니다.|  
|**Enqueued P10 Msgs/sec**|인스턴스의 큐에 배치된 우선 순위가 10인 초당 메시지 조각의 수입니다.|  
|**Enqueued Transmission Msgs/sec**|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 전송 큐에 배치된 초당 메시지의 수입니다.|  
|**Enqueued Transport Msg Frag Tot**|인스턴스의 큐에 배치된 메시지 조각의 수로 네트워크를 통해 도착한 메시지만 계산합니다.|  
|**Enqueued Transport Msg Frags/sec**|인스턴스의 큐에 배치된 초당 메시지 조각의 수입니다.|  
|**Enqueued Transport Msgs Total**|인스턴스의 큐에 배치된 메시지의 수로 네트워크를 통해 도착한 메시지만 계산합니다.|  
|**Enqueued Transport Msgs/sec**|인스턴스의 큐에 배치된 초당 메시지의 수로 네트워크를 통해 도착한 메시지만 계산합니다.|  
|**Forwarded Messages Total**|이 컴퓨터에서 전달한 총 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 메시지 수입니다.|  
|**Enqueued Messages/sec**|이 컴퓨터에서 전달한 초당 메시지의 수입니다.|  
|**Forwarded Msg Byte Total**|이 컴퓨터에서 전달한 총 메시지 크기(바이트)입니다.|  
|**Forwarded Msg Bytes/sec**|이 컴퓨터에서 전달한 초당 메시지 크기(바이트)입니다.|  
|**Forwarded Msg Discarded Total**|이 컴퓨터가 전달하기 위해 받았으나 성공적으로 전달하지 못한 메시지 수입니다.|  
|**Forwarded Msg Discarded/sec**|이 컴퓨터가 전달하기 위해 받았으나 성공적으로 전달하지 못한 초당 메시지 수입니다.|  
|**Forwarded Pending Msg Bytes**|현재 전달하기 위해 보유하고 있는 총 메시지 크기입니다.|  
|**Forwarded Pending Msg Count**|현재 전달하기 위해 보유하고 있는 총 메시지의 수입니다.|  
|**SQL RECEIVE Total**|처리된 총 [!INCLUDE[tsql](../../includes/tsql-md.md)] RECEIVE 문의 수입니다.|  
|**SQL RECEIVEs/sec**|초당 처리된 [!INCLUDE[tsql](../../includes/tsql-md.md)] RECEIVE 문의 수입니다.|  
|**SQL SEND Total**|실행된 총 [!INCLUDE[tsql](../../includes/tsql-md.md)] SEND 문의 수입니다.|  
|**SQL SENDs/sec**|초당 실행된 [!INCLUDE[tsql](../../includes/tsql-md.md)] SEND 문의 수입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
