---
title: SQL Server, Availability Replica | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- performance counters [SQL Server], AlwaysOn Availability Groups
- SQLServer:Availability Replica
- Availability Groups [SQL Server], performance counters
ms.assetid: e402f996-c1fb-484a-b804-45c49972f2e0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 442501dad8dfffb06ba9d5f82674269011b59007
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48055609"
---
# <a name="sql-server-availability-replica"></a>SQL Server, 가용성 복제본
  **SQLServer:Availability Replica** 성능 개체는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 AlwaysOn 가용성 그룹의 가용성 복제본에 대한 정보를 보고하는 성능 카운터를 포함합니다. 모든 가용성 복제본 성능 카운터는 로컬 복제본을 반영하는 보내기/받기 카운터와 함께 주 복제본과 보조 복제본 모두에 적용됩니다. 대부분의 경우 주 복제본은 대부분의 데이터를 보내고 보조 복제본은 해당 데이터를 받습니다. 그러나 보조 복제본은 주 복제본에 ACK 및 일부 다른 백그라운드 트래픽을 보냅니다. 특정 가용성 복제본에서 일부 카운터는 로컬 복제본의 현재 역할(주/보조)에 따라 값을 0으로 표시합니다.  
  
|카운터 이름|Description|  
|------------------|-----------------|  
|**Bytes Received from Replica/sec**|초당 가용성 복제본으로부터 받은 바이트 수입니다. ping 및 상태 업데이트를 수행하면 사용자 업데이트가 없는 데이터베이스에서도 네트워크 트래픽이 생성됩니다.|  
|**Bytes Sent to Replica/sec**|초당 원격 가용성 복제본으로 보낸 바이트 수입니다. 주 복제본의 경우, 보조 복제본으로 보낸 바이트 수입니다. 보조 복제본의 경우, 주 복제본으로 보낸 바이트 수입니다.|  
|**Bytes Sent to Transport/sec**|네트워크를 통해 초당 원격 가용성 복제본으로 보낸 실제 바이트 수입니다. 주 복제본의 경우, 보조 복제본으로 보낸 바이트 수입니다. 보조 복제본의 경우, 주 복제본으로 보낸 바이트 수입니다.|  
|**Flow Control Time (ms/sec)**|마지막 1초 동안 로그 스트림 메시지가 전송 흐름 제어를 기다린 시간(밀리초)입니다.|  
|**Flow Control/sec**|마지막 1초 동안 시작된 흐름 제어 횟수입니다. **Flow Control Time (ms/sec)** 을 **Flow Control/sec** 로 나눈 값이 평균 대기 시간입니다.|  
|**Receives from Replica/sec**|초당 복제본으로부터 받은 AlwaysOn 메시지의 수입니다.|  
|**Resent Messages/sec**|마지막 1초 동안 다시 보낸 AlwaysOn 메시지의 수입니다.|  
|**Sends to Replica/sec**|초당 이 가용성 복제본으로 보낸 AlwaysOn 메시지의 수입니다.|  
|**Sends to Transport/sec**|네트워크를 통해 초당 원격 가용성 복제본으로 보낸 AlwaysOn 메시지의 실제 수입니다. 주 복제본의 경우, 보조 복제본으로 보낸 메시지 수입니다. 보조 복제본의 경우, 주 복제본으로 보낸 메시지 수입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Serve, 데이터베이스 복제본](sql-server-database-replica.md)   
 [AlwaysOn 가용성 그룹 (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
