---
title: 데이터베이스 미러링 세션 수동 장애 조치(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- failover [SQL Server], database mirroring
- manual failover [SQL Server]
- database mirroring [SQL Server], failover
ms.assetid: 36218d61-b5f5-4194-905a-608e0e903db4
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: a78dc1647095f5ef444713a7ad46f12e45fc7c65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36081922"
---
# <a name="manually-fail-over-a-database-mirroring-session-transact-sql"></a>데이터베이스 미러링 세션 수동 장애 조치(Transact-SQL)
  미러된 데이터베이스가 동기화되면, 즉 데이터베이스가 SYNCHRONIZED 상태인 경우 데이터베이스 소유자가 미러 서버에 수동 장애 조치(failover)를 시작할 수 있습니다. 수동 장애 조치는 주 서버에서만 시작할 수 있습니다.  
  
### <a name="to-manually-fail-over-a-database-mirroring-session"></a>데이터베이스 미러링 세션을 수동 장애 조치하려면  
  
1.  주 서버를 연결합니다.  
  
2.  데이터베이스 컨텍스트를 **master** 데이터베이스로 설정합니다.  
  
     `USE master;`  
  
3.  주 서버에서 다음 문을 실행합니다.  
  
     [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring) *database_name* SET PARTNER FAILOVER. 여기서 *database_name* 은 미러된 데이터베이스입니다.  
  
     이렇게 하면 미러 서버가 주 역할로 즉시 전환하기 시작합니다.  
  
 이전 주 서버에서 클라이언트는 데이터베이스에서 연결이 끊어지고 진행 중인 트랜잭션은 롤백됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] DTC(Distributed Transaction Coordinator)를 사용하여 준비되었지만 장애 조치가 발생했을 때 커밋되지 않은 트랜잭션은 데이터베이스에 장애 조치를 취한 다음 중단된 것으로 간주됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE 데이터베이스 미러링&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-database-mirroring)   
 [데이터베이스 미러링 세션 수동 장애 조치&#40;SQL Server Management Studio&#41;](manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)   
 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)  
  
  
