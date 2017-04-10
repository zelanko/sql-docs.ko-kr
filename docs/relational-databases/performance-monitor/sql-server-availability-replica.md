---
title: "SQL Server, 가용성 복제본 | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "가용성 그룹 [SQL Server], 모니터링"
  - "성능 카운터 [SQL Server], AlwaysOn 가용성 그룹"
  - "SQLServer:가용성 복제본"
  - "가용성 그룹 [SQL Server], 성능 카운터"
ms.assetid: e402f996-c1fb-484a-b804-45c49972f2e0
caps.latest.revision: 25
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 25
---
# SQL Server, 가용성 복제본
  **SQLServer:Availability Replica** 성능 개체는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 Always On 가용성 그룹의 가용성 복제본에 대한 정보를 보고하는 성능 카운터를 포함합니다. 모든 가용성 복제본 성능 카운터는 로컬 복제본을 반영하는 보내기/받기 카운터와 함께 주 복제본과 보조 복제본 모두에 적용됩니다. 대부분의 경우 주 복제본은 대부분의 데이터를 보내고 보조 복제본은 해당 데이터를 받습니다. 그러나 보조 복제본은 주 복제본에 ACK 및 일부 다른 백그라운드 트래픽을 보냅니다. 특정 가용성 복제본에서 일부 카운터는 로컬 복제본의 현재 역할(주/보조)에 따라 값을 0으로 표시합니다.  
  
|카운터 이름|Description|  
|------------------|-----------------|  
|**Bytes Received from Replica/sec**|초당 가용성 복제본으로부터 받은 바이트 수입니다. ping 및 상태 업데이트를 수행하면 사용자 업데이트가 없는 데이터베이스에서도 네트워크 트래픽이 생성됩니다.|  
|**Bytes Sent to Replica/sec**|초당 원격 가용성 복제본으로 보낸 바이트 수입니다. 주 복제본의 경우, 보조 복제본으로 보낸 바이트 수입니다. 보조 복제본의 경우, 주 복제본으로 보낸 바이트 수입니다.|  
|**Bytes Sent to Transport/sec**|네트워크를 통해 초당 원격 가용성 복제본으로 보낸 실제 바이트 수입니다. 주 복제본의 경우, 보조 복제본으로 보낸 바이트 수입니다. 보조 복제본의 경우, 주 복제본으로 보낸 바이트 수입니다.|  
|**Flow Control Time (ms/sec)**|마지막 1초 동안 로그 스트림 메시지가 전송 흐름 제어를 기다린 시간(밀리초)입니다.|  
|**Flow Control/sec**|마지막 1초 동안 시작된 흐름 제어 횟수입니다. **Flow Control Time (ms/sec)**을 **Flow Control/sec**로 나눈 값이 평균 대기 시간입니다.|  
|**Receives from Replica/sec**|초당 복제본으로부터 받은 Always On 메시지의 수입니다.|  
|**Resent Messages/sec**|마지막 1초 동안 다시 보낸 Always On 메시지의 수입니다.|  
|**Sends to Replica/sec**|초당 이 가용성 복제본으로 보낸 Always On 메시지의 수입니다.|  
|**Sends to Transport/sec**|네트워크를 통해 초당 원격 가용성 복제본으로 보낸 Always On 메시지의 실제 수입니다. 주 복제본의 경우, 보조 복제본으로 보낸 메시지 수입니다. 보조 복제본의 경우, 주 복제본으로 보낸 메시지 수입니다.|  
  
## 관련 항목:  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Serve, 데이터베이스 복제본](../../relational-databases/performance-monitor/sql-server-database-replica.md)   
 [Always On 가용성 그룹(SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx)  
  
  