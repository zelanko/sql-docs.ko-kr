---
title: SQL Server, Database Mirroring 개체 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Database Mirroring
- database mirroring [SQL Server], performance counters
- performance counters [SQL Server], database mirroring
- Database Mirroring object
ms.assetid: a27b51ee-7637-4525-9424-bcc16947dc13
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 95d7bb5d1d071cab0c791a958a5e2f61fea41af5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85038667"
---
# <a name="sql-server-database-mirroring-object"></a>SQL Server, Database Mirroring 개체
  **SQLServer:Database Mirroring** 성능 개체는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 미러링에 대한 정보를 보고하는 성능 카운터를 포함합니다. 다음 표에서는 이 개체가 포함하는 카운터를 나열합니다.  
  
|속성|Description|  
|----------|-----------------|  
|**Bytes Received/sec**|초당 받은 바이트 수입니다.|  
|**Bytes Sent/sec**|초당 보낸 바이트 수입니다.|  
|**Log Bytes Received/sec**|초당 받은 로그 바이트 수입니다.|  
|**Log Bytes Redone from Cache/sec**|마지막 1초 동안 미러링 로그 캐시에서 가져온 다시 실행된 로그 바이트 수입니다.<br /><br /> 이 카운터는 미러 서버에서만 사용됩니다. 주 서버에서 이 값은 항상 0입니다.|  
|**Log Bytes Sent from Cache/sec**|마지막 1초 동안 미러링 로그 캐시에서 가져온 전송된 로그 바이트 수입니다.<br /><br /> 이 카운터는 주 서버에서만 사용됩니다. 미러 서버에서 이 값은 항상 0입니다.|  
|**Log Bytes Sent/sec**|초당 보낸 로그 바이트 수입니다.|  
|**Log Compressed Bytes Rcvd/sec**|마지막 1초 동안 받은 로그의 압축된 바이트 수입니다.|  
|**Log Compressed Bytes Sent/sec**|마지막 1초 동안 보낸 로그의 압축된 바이트 수입니다.|  
|**Log Harden Time (ms)**|마지막 1초 동안 로그 블록이 디스크에 확정될 때까지 기다린 시간(밀리초)입니다.|  
|**Log Remaining for Undo KB**|장애 조치(Failover) 후 새 미러 서버에서 아직 검색되지 않고 남아 있는 로그의 총 KB 수입니다.<br /><br /> 이 카운터는 실행 취소 단계 동안 미러 서버에서만 사용됩니다. 실행 취소 단계가 완료되면 카운터가 0으로 다시 설정됩니다. 주 서버에서 이 값은 항상 0입니다.|  
|**Log Scanned for Undo KB**|장애 조치 후 새 미러 서버에서 검색된 로그의 총 KB 수입니다.<br /><br /> 이 카운터는 실행 취소 단계 동안 미러 서버에서만 사용됩니다. 실행 취소 단계가 완료되면 카운터가 0으로 다시 설정됩니다. 주 서버에서 이 값은 항상 0입니다.|  
|**Log Send Flow Control Time (ms)**|마지막 1초 동안 로그 스트림 메시지가 전송 흐름 제어를 기다린 시간(밀리초)입니다.<br /><br /> 로그 데이터와 메타데이터를 미러링 파트너로 보내는 것은 데이터베이스 미러링에서 가장 데이터를 많이 사용하는 작업이며 데이터베이스 미러링 및 Service Broker 송신 버퍼를 독점할 수 있습니다. 이 카운터를 사용하여 데이터베이스 미러링 세션별로 이 버퍼의 사용을 모니터링할 수 있습니다.|  
|**Log Send Queue KB**|미러 서버로 아직 보내지 않은 로그의 총 KB 수입니다.|  
|**Mirrored Write Transactions/sec**|마지막 1초 동안 미러된 데이터베이스에 썼으며 커밋을 위해 로그가 미러로 전송될 때까지 기다린 트랜잭션 수입니다.<br /><br /> 이 카운터는 주 서버가 로그 레코드를 미러 서버로 보내는 경우에만 증가됩니다.|  
|**Pages Sent/sec**|초당 보낸 페이지 수입니다.|  
|**Receives/sec**|초당 받은 미러링 메시지 수입니다.|  
|**Redo Bytes/sec**|초당 미러 데이터베이스에서 롤포워드한 로그 바이트 수입니다.|  
|**Redo Queue KB**|현재 미러 데이터베이스에 적용하여 롤포워드해야 할 확정된 로그의 총 KB 수입니다. 이것은 미러 데이터베이스에서 주 데이터베이스로 보내집니다.|  
|**Send/Receive Ack Time**|마지막 1초 동안 메시지가 파트너의 승인을 기다린 시간(밀리초)입니다.<br /><br /> 이 카운터는 설명이 없는 장애 조치, 큰 Send Queue 또는 긴 트랜잭션 대기 시간과 같이 네트워크 병목 상태로 인해 발생할 수 있는 문제를 해결하는 데 도움이 됩니다. 이러한 경우 이 카운터의 값을 분석하여 네트워크에서 문제를 일으키는지 여부를 확인할 수 있습니다.|  
|**Sends/sec**|초당 보낸 미러링 메시지 수입니다.|  
|**Transaction Delay**|종료되지 않은 커밋 승인을 기다리는 지연 시간입니다.|  
  
> [!NOTE]  
>  각 파트너에서 일부 카운터는 파트너가 현재 수행하고 있는 역할에 따라 0 값을 표시합니다.  
  
## <a name="remarks"></a>설명  
 성능 카운터를 사용하면 데이터베이스 미러링 성능을 모니터링할 수 있습니다. 예를 들어 **Transaction Delay** 카운터를 사용하면 데이터베이스 미러링이 주 서버의 성능에 영향을 주는지 여부를 알 수 있고 **Redo Queue** 와 **Log Send Queue** 카운터를 사용하면 미러 데이터베이스가 주 데이터베이스와 동기화가 제대로 이루어지는지 알 수 있습니다. **Log Bytes Sent/sec** 카운터를 사용하면 초당 보낸 로그의 양을 모니터링할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)  
  
  
