---
title: 데이터베이스 미러링 세션에 서비스 강제 수행(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- forced service [SQL Server]
- database mirroring [SQL Server], forcing service
ms.assetid: 8b6ffe77-35f3-4e2a-a658-8a38a8e1c794
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ef1a7101a0bd16c3ee2868f47a8dc15f29092621
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101423"
---
# <a name="force-service-in-a-database-mirroring-session-transact-sql"></a>데이터베이스 미러링 세션에 서비스 강제 수행(Transact-SQL)
  성능 우선 모드 및 장애 조치를 지원하지 않는 보호 우선 모드에서 미러 서버는 사용할 수 있는데 주 서버는 실패하는 경우 데이터베이스 소유자는 서비스가 미러 데이터베이스로 장애 조치(데이터 손실 가능)되도록 강제 적용하여 데이터베이스를 사용 가능하게 만들 수 있습니다. 이 옵션은 다음 조건이 모두 충족된 경우에만 사용할 수 있습니다.  
  
-   주 서버가 다운되었습니다.  
  
-   WITNESS가 OFF로 설정되거나 미러 서버에 연결되어 있습니다.  
  
> [!CAUTION]  
>  엄밀히 말하면 강제 서비스는 재해 복구 수단이라 할 수 있습니다. 서비스를 강제 적용하면 데이터가 손실될 수 있습니다. 따라서 데이터베이스로 서비스를 즉시 복원하기 위해 일부 데이터가 손실되는 위험을 감수하려는 경우에만 서비스를 강제 수행합니다. 강제 서비스로 인해 중요한 데이터가 손실될 위험이 있는 경우에는 미러링을 중지하고 데이터베이스를 수동으로 다시 동기화하는 것이 좋습니다. 강제 서비스의 위험성에 대한 자세한 내용은 [Database Mirroring Operating Modes](database-mirroring-operating-modes.md)를 참조하십시오.  
  
 서비스를 강제 적용하면 세션이 일시 중지되고 새 복구 분기가 시작됩니다. 서비스를 강제 적용하는 것은 미러링을 제거하고 이전 주 데이터베이스를 복구하는 것과 유사합니다. 그러나 강제 서비스의 경우 미러링을 재개할 때 데이터베이스를 다시 동기화하기 때문에 데이터가 손실될 가능성이 있습니다.  
  
### <a name="to-force-service-in-a-database-mirroring-session"></a>데이터베이스 미러링 세션에서 서비스를 강제 수행하려면  
  
1.  미러 서버로 연결합니다.  
  
2.  다음 문을 실행합니다.  
  
     ALTER DATABASE *<database_name>* SET PARTNER FORCE_SERVICE_ALLOW_DATA_LOSS  
  
     여기서 *<database_name>* 은 미러 데이터베이스입니다.  
  
     미러 서버는 주 서버로 바로 전환되고 미러링은 일시 중지됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [데이터베이스 미러링 운영 모드](database-mirroring-operating-modes.md)  
  
  
