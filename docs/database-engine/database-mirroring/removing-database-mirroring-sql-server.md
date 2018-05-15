---
title: 데이터베이스 미러링 제거(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: high-availability
ms.component: database-mirroring
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], removing
- stopping database mirroring [SQL Server]
- removing database mirroring [SQL Server]
ms.assetid: 40c72091-8f03-4037-8b55-5e95309fe145
caps.latest.revision: 32
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e7538fb9a9ca57db71f6e49f6e299764412199ec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="removing-database-mirroring-sql-server"></a>데이터베이스 미러링 제거(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  데이터베이스 소유자는 언제든지 파트너에서 데이터베이스 미러링 세션을 수동으로 중지할 수 있습니다.  
  
## <a name="impact-of-removing-mirroring"></a>미러링 제거의 영향  
 미러링을 제거하면 다음과 같은 결과가 발생합니다.  
  
-   파트너 간의 관계 및 각 파트너와 미러링 모니터 서버 간의 관계가 영구적으로 해제됩니다(관계가 있는 경우).  
  
     세션이 중지될 때 파트너가 서로 통신하고 있으면 두 컴퓨터에서 해당 관계가 즉시 해제됩니다. 파트너가 서로 통신하고 있지 않으면(세션 중지 시 데이터베이스는 DISCONNECTED 상태임) 미러링이 중지된 파트너에서 해당 관계가 즉시 해제됩니다. 상대 파트너가 다시 연결을 시도할 경우 데이터베이스 미러링 세션이 종료되었음을 확인하게 됩니다.  
  
-   세션을 일시 중지하는 경우와 달리 미러링 세션에 대한 정보가 삭제됩니다. 미러링은 주 데이터베이스와 미러 데이터베이스에서 모두 제거됩니다. **sys.databases**에서 **mirroring_state** 열과 다른 모든 미러링 열은 NULL로 설정됩니다. 자세한 내용은 [sys.database_mirroring&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)을 참조하세요.  
  
-   각 파트너 서버 인스턴스는 별도의 데이터베이스 복사본으로 남겨집니다.  
  
-   미러 데이터베이스가 RESTORE WITH NORECOVERY를 사용하여 생성되었기 때문에 RESTORING 상태( **sys.databases** 의 **state**열 참조)로 남게 됩니다. 따라서 이전 미러 데이터베이스를 삭제하거나 WITH RECOVERY를 사용하여 복원할 수 있습니다. 데이터베이스를 복구할 때 새로운 복구 분기 지점에서 복구를 시작하므로 이전 주 데이터베이스에서 갈라져 나옵니다.  
  
> [!NOTE]  
>  세션을 중지한 후에 미러링을 계속하려면 데이터베이스 미러링 세션을 새로 설정해야 합니다. 미러링을 중지한 후에 로그 백업을 만들 경우 이 로그 백업을 미러 데이터베이스에 적용한 후에 미러링을 다시 시작해야 합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **데이터베이스 미러링을 제거하려면**  
  
-   [데이터베이스 미러링 제거&#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-database-mirroring-sql-server.md)  
  
 **데이터베이스 미러링을 시작하려면**  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)  
  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE 데이터베이스 미러링&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [데이터베이스 미러링 일시 중지 및 재개&#40;SQL Server&#41;](../../database-engine/database-mirroring/pausing-and-resuming-database-mirroring-sql-server.md)   
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
  
