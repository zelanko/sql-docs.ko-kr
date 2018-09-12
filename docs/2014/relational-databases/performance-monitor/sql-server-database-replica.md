---
title: SQL Server, Database Replica | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], monitoring
- SQLServer:Database Replica
- performance counters [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], performance counters
ms.assetid: a5f6bdce-2b13-4924-aaeb-b50b57d624d8
caps.latest.revision: 25
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4edbe5037b638b7bdd17de77b849bd64df27d398
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43808219"
---
# <a name="sql-server-database-replica"></a>SQL Server, 데이터베이스 복제본
  **SQLServer: 데이터베이스 복제본** 성능 개체는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 AlwaysOn 가용성 그룹의 보조 데이터베이스에 대한 정보를 보고하는 성능 카운터를 포함합니다. 이 개체는 보조 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서만 유효합니다.  
  
|카운터 이름|Description|표시 대상|  
|------------------|-----------------|--------------|  
|**File Bytes Received/sec**|마지막 1초 동안 보조 데이터베이스에 대해 보조 복제본에서 받은 FILESTREAM 데이터의 양입니다.|보조 복제본|  
|**Log Bytes Received/sec**|마지막 1초 동안 데이터베이스에 대해 보조 복제본에서 받은 로그 레코드의 양입니다.|보조 복제본|  
|**Log remaining for undo**|실행 취소 단계를 완료하기까지 남은 로그의 양(KB)입니다.|보조 복제본|  
|**Log Send Queue**|주 데이터베이스의 로그 파일에 있는 로그 레코드 중 아직 보조 복제본으로 전송되지 않은 레코드의 양(KB)입니다. 이 값은 주 복제본에서 보조 복제본으로 전송됩니다. 보조 복제본으로 전송되는 FILESTREAM 파일은 큐 크기에 포함되지 않습니다.|보조 복제본|  
|**Mirrored Write Transactions/sec**|주 데이터베이스에 기록된 다음 마지막 1초 동안 로그가 보조 데이터베이스에 전송될 때까지 커밋을 기다린 트랜잭션 수입니다.|주 복제본|  
|**Recovery Queue**|아직 다시 실행되지 않은 보조 복제본의 로그 파일에 있는 로그 레코드의 양입니다.|보조 복제본|  
|**초당 차단된 다시 실행**|데이터베이스 독자가 보유한 잠금에서 다시 실행 스레드가 차단되는 횟수입니다.|보조 복제본|  
|**Redo Bytes Remaining**|되돌리기 단계를 완료하기 위해 다시 실행할 남은 로그 양(KB)입니다.|보조 복제본|  
|**Redone Bytes/sec**|마지막 1초 동안 보조 데이터베이스에서 다시 실행된 로그 레코드의 양입니다.|보조 복제본|  
|**Total Log requiring undo**|실행 취소해야 하는 로그의 총 크기(KB)입니다.|보조 복제본|  
|**Transaction Delay**|종료되지 않은 커밋 승인을 기다리는 지연 시간(밀리초)입니다.|주 복제본|  
  
## <a name="see-also"></a>관련 항목  
 [리소스 사용 모니터링&#40;시스템 모니터&#41;](monitor-resource-usage-system-monitor.md)   
 [SQL Server, 가용성 복제본](sql-server-availability-replica.md)   
 [SQL Server, Databases 개체](sql-server-databases-object.md)   
 [AlwaysOn 가용성 그룹 (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
