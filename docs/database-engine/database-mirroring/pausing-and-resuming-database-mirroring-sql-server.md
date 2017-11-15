---
title: "데이터베이스 미러링 일시 중지 및 재개(SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sessions [SQL Server], database mirroring
- resuming database mirroring
- database mirroring [SQL Server], pausing
- database mirroring [SQL Server], resuming
- pausing database mirroring
ms.assetid: c67802c6-ee8c-4cbd-a6d4-f7b80413a4ab
caps.latest.revision: "32"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 285a9cf5c006787b371411c1eb2e1bd5c07ff050
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="pausing-and-resuming-database-mirroring-sql-server"></a>데이터베이스 미러링 일시 중지 및 재개(SQL Server)
  데이터베이스 소유자는 데이터베이스 미러링 세션을 일시 중지하고 나중에 언제든지 재개할 수 있습니다. 일시 중지하면 미러링을 일시 중지하는 동안 세션 상태가 유지됩니다. 병목 상태에서 일시 중지는 주 서버의 성능을 높이는 데 유용할 수 있습니다.  
  
 세션을 일시 중지한 상태에서도 주 데이터베이스는 사용할 수 있습니다. 세션을 일시 중지하면 미러링 세션의 상태가 SUSPENDED로 설정되고 미러 데이터베이스가 주 데이터베이스보다 뒤쳐지므로 노출된 상태로 주 데이터베이스가 실행됩니다.  
  
 일시 중지된 세션을 빨리 재개하는 것이 좋습니다. 데이터베이스 미러링 세션이 일시 중지된 동안에는 트랜잭션 로그를 자를 수 없으므로 데이터베이스 미러링 세션을 너무 오래 일시 중지하면 트랜잭션 로그가 꽉 차서 데이터베이스를 사용할 수 없게 됩니다. 이렇게 되는 이유에 대한 자세한 내용은 뒤에 나오는 "로그 잘림에 대한 일시 중지 및 재개의 영향"을 참조하세요.  
  
> [!IMPORTANT]  
>  강제 서비스에 따라 원래 주 서버가 다시 연결되면 미러링이 일시 중지됩니다. 이 경우 미러링을 재개하면 원래 주 서버의 데이터가 손실될 수 있습니다. 데이터 손실 위험을 관리하는 방법은 [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)를 참조하세요.  
  
 **항목 내용**  
  
-   [로그 잘림에 대한 일시 중지 및 재개의 영향](#EffectOnLogTrunc)  
  
-   [꽉 찬 트랜잭션 로그 방지](#AvoidFullLog)  
  
-   [관련 태스크](#RelatedTasks)  
  
##  <a name="EffectOnLogTrunc"></a> 로그 잘림에 대한 일시 중지 및 재개의 영향  
 일반적으로 데이터베이스에서 자동 검사점을 수행하면 다음 로그 백업 이후 해당 트랜잭션 로그가 이 검사점까지 잘립니다. 데이터베이스 미러링 세션이 일시 중지된 동안에는 주 서버가 현재 로그 레코드를 미러 서버로 보내기 위해 대기 중이므로 모두 활성 상태로 유지됩니다. 보내지 않은 로그 레코드는 세션이 재개되어 주 서버에서 해당 로그 레코드를 미러 서버로 보낼 때까지 주 데이터베이스의 트랜잭션 로그에 누적됩니다.  
  
 세션이 재개되면 주 서버에서 즉시 누적된 로그 레코드를 미러 서버로 보내기 시작합니다. 미러 서버가 가장 오래된 자동 검사점에 해당하는 로그 레코드를 큐에 대기했음을 확인하면 주 서버에서 주 데이터베이스의 로그를 해당 검사점까지 자릅니다. 미리 서버는 동일한 로그 레코드에서 Redo Queue를 자릅니다. 연속된 각 검사점에 대해 이 프로세스가 반복되므로 로그는 검사점을 기준으로 단계별로 잘립니다.  
  
> [!NOTE]  
>  검사점 및 로그 잘림에 대한 자세한 내용은 [데이터베이스 검사점&#40;SQL Server&#41;](../../relational-databases/logs/database-checkpoints-sql-server.md)을 참조하세요.  
  
##  <a name="AvoidFullLog"></a> 꽉 찬 트랜잭션 로그 방지  
 서버 인스턴스의 공간이 부족하거나 최대 크기에 도달하여 로그가 가득 차면 데이터베이스는 더 이상 업데이트를 수행할 수 없습니다. 이 문제를 피하는 방법은 두 가지가 있습니다.  
  
-   로그가 가득 차기 전에 데이터베이스 미러링 세션을 재개하거나 로그 공간을 추가합니다. 데이터베이스 미러링을 재개하면 주 서버는 누적된 활성 로그를 미러 서버로 전송하고 미러 데이터베이스는 SYNCHRONIZING 상태가 됩니다. 그러면 미러 서버에서 로그를 디스크에 확정하고 다시 실행을 시작할 수 있습니다.  
  
-   미러링을 제거하여 데이터베이스 미러링 세션을 중지합니다.  
  
     일시 중지와는 달리 미러링을 제거하면 미러링 세션에 관한 모든 정보가 삭제됩니다. 각 파트너 서버 인스턴스는 데이터베이스의 자체 복사본을 유지합니다. 이전 미러 복사본을 복구하면 이전 주 복사본과 달라져서 세션이 일시 중지된 후 경과한 시간만큼 지연됩니다. 자세한 내용은 [데이터베이스 미러링 제거&#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)를 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **데이터베이스 미러링을 일시 중지 또는 재개하려면**  
  
-   [데이터베이스 미러링 세션 일시 중지 또는 재개&#40;SQL Server&#41;](../../database-engine/database-mirroring/pause-or-resume-a-database-mirroring-session-sql-server.md)  
  
 **데이터베이스 미러링을 중지하려면**  
  
-   [데이터베이스 미러링 제거&#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-database-mirroring-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [데이터베이스 미러링 제거&#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)  
  
  
