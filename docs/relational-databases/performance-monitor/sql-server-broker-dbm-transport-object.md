---
title: SQL Server, Broker - DBM Transport 개체 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance-monitor
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Broker / DBM Transport object
- SQLServer:Broker/DBM Transport
ms.assetid: eddb60b6-20a9-416c-adf3-4bc1687944fa
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: caedbed7827753bcd099103d6d70d4f99d447048
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sql-server-broker---dbm-transport-object"></a>SQL Server, Broker - DBM Transport 개체
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **Broker / DBM Transport** 성능 개체에는 Service Broker 및 데이터베이스 미러링에 대한 네트워킹 정보를 보고하는 성능 카운터가 들어 있습니다. 다음 표에서는 이 개체가 포함하는 카운터를 나열합니다.  
  
|SQL Server Broker / DBM Transport 카운터|Description|  
|------------------------------------------------|-----------------|  
|**Current Bytes for Recv I/O**|이 카운터는 현재 실행 중인 전송 수신 작업에서 읽을 바이트 수를 보고합니다.|  
|**Current Bytes for Send I/O**|이 카운터는 현재 네트워크로 전송 중인 메시지 조각의 바이트 수를 보고합니다.|  
|**Current Msg Frags for Send I/O**|이 카운터는 네트워크로 전송 중인 메시지 조각의 총 수를 보고합니다.|  
|**Message Fragment P1 Sends/sec**|이 카운터는 초당 네트워크로 보낸 우선 순위가 1인 메시지 조각의 수를 보고합니다.|  
|**Message Fragment P2 Sends/sec**|이 카운터는 초당 네트워크로 보낸 우선 순위가 2인 메시지 조각의 수를 보고합니다.|  
|**Message Fragment P3 Sends/sec**|이 카운터는 초당 네트워크로 보낸 우선 순위가 3인 메시지 조각의 수를 보고합니다.|  
|**Message Fragment P4 Sends/sec**|이 카운터는 초당 네트워크로 보낸 우선 순위가 4인 메시지 조각의 수를 보고합니다.|  
|**Message Fragment P5 Sends/sec**|이 카운터는 초당 네트워크로 보낸 우선 순위가 5인 메시지 조각의 수를 보고합니다.|  
|**Message Fragment P6 Sends/sec**|이 카운터는 초당 네트워크로 보낸 우선 순위가 6인 메시지 조각의 수를 보고합니다.|  
|**Message Fragment P7 Sends/sec**|이 카운터는 초당 네트워크로 보낸 우선 순위가 7인 메시지 조각의 수를 보고합니다.|  
|**Message Fragment P8 Sends/sec**|이 카운터는 초당 네트워크로 보낸 우선 순위가 8인 메시지 조각의 수를 보고합니다.|  
|**Message Fragment P9 Sends/sec**|이 카운터는 초당 네트워크로 보낸 우선 순위가 9인 메시지 조각의 수를 보고합니다.|  
|**Message Fragment P10 Sends/sec**|이 카운터는 초당 네트워크로 보낸 우선 순위가 10인 메시지 조각의 수를 보고합니다.|  
|**Message Fragment Receives/sec**|이 카운터는 초당 네트워크를 통해 받은 메시지 조각의 수를 보고합니다.|   
|**Message Fragment Sends/sec**|이 카운터는 초당 네트워크로 보낸 모든 우선 순위의 메시지 조각의 수를 보고합니다.|  
|**Msg Fragment Recv Size Avg**|이 카운터는 네트워크를 통해 받은 메시지 조각의 평균 크기를 보고합니다.|  
|**Msg Fragment Recv Size Avg Base**|내부용으로만 사용할 수 있습니다.| 
|**Msg Fragment Send Size Avg**|이 카운터는 네트워크로 보낸 메시지 조각의 평균 크기를 보고합니다.|  
|**Msg Fragment Send Size Avg Base**|내부용으로만 사용할 수 있습니다.|
|**Open Connection Count**|이 카운터는 현재 Service Broker에서 연 네트워크 연결 수를 보고합니다.|  
|**Pending Bytes for Recv I/O**|이 카운터는 네트워크에서 받았지만 아직 큐에 저장되지 않았거나 삭제되지 않은 메시지 조각에 포함된 바이트 수를 보고합니다.|  
|**Pending Bytes for Send I/O**|이 카운터는 네트워크로 보낼 준비가 된 메시지 조각의 총 바이트 수를 보고합니다.|  
|**Pending Msg Frags for Recv I/O**|이 카운터는 네트워크에서 받았지만 아직 큐에 저장되지 않았거나 삭제되지 않은 메시지 조각의 수를 보고합니다.|  
|**Pending Msg Frags for Send I/O**|이 카운터는 네트워크로 보낼 준비가 된 총 메시지 조각 수를 보고합니다.|  
|**Receive I/O bytes/sec**|이 카운터는 Service Broker 끝점과 데이터베이스 미러링 끝점에서 네트워크를 통해 받은 초당 바이트 수를 보고합니다.|  
|**Receive I/O Bytes Total**|이 카운터는 Service Broker 끝점과 데이터베이스 미러링 끝점에서 네트워크를 통해 받은 총 바이트 수를 보고합니다.|  
|**Receive I/O Len Avg**|이 카운터는 전송 수신 작업의 평균 바이트 수를 보고합니다.|  
|**Receive I/O Len Avg Base**|내부용으로만 사용할 수 있습니다.|
|**Receive I/Os/sec**|이 카운터는 Service Broker/DBM 전송 계층에서 완료한 초당 전송 수신 I/O 작업의 수를 보고합니다. 전송 수신 작업에는 둘 이상의 메시지 조각이 포함될 수 있습니다.|  
|**Recv I/O Buffer Copies bytes/sec**|전송 수신 I/O 작업이 메모리에서 버퍼 조각을 이동한 속도입니다.|
|**Recv I/O Buffer Copies Count**|전송 수신 I/O 작업이 메모리에서 버퍼 조각을 이동한 횟수입니다.| 
|**Send I/O bytes/sec**|이 카운터는 Service Broker 끝점과 데이터베이스 미러링 끝점에서 네트워크를 통해 보낸 초당 바이트 수를 보고합니다.|   
|**Send I/O Bytes Total**|이 카운터는 Service Broker 끝점과 데이터베이스 미러링 끝점에서 네트워크를 통해 보내 총 바이트 수를 보고합니다.| 
|**Send I/O Len Avg**|이 카운터는 각 전송 송신 작업의 평균 크기를 바이트로 보고합니다. 전송 송신 작업에는 둘 이상의 메시지 조각이 포함될 수 있습니다.|  
|**Send I/O Len Avg Base**|내부용으로만 사용할 수 있습니다.|
|**Send I/Os/sec**|이 카운터는 완료된 초당 전송 송신 I/O 작업의 수를 보고합니다. 전송 송신 작업에는 둘 이상의 메시지 조각이 포함될 수 있습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [sys.dm_broker_forwarded_messages&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-broker-forwarded-messages-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
