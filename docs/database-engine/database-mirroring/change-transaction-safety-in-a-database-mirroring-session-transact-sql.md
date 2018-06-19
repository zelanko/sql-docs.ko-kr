---
title: 데이터베이스 미러링 세션에서 트랜잭션 보안 변경(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: high-availability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- transaction safety [SQL Server database mirroring]
ms.assetid: 8b03bb82-8589-4558-8545-9942fe008391
caps.latest.revision: 38
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 250d077becd2261c98f14f062b3d490a71f7a5fe
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35311482"
---
# <a name="change-transaction-safety-in-a-database-mirroring-session-transact-sql"></a>데이터베이스 미러링 세션에서 트랜잭션 보안 변경(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  트랜잭션 보안은 세션의 운영 모드를 제어하는 특성입니다. 그러나 데이터베이스 소유자는 언제든지 트랜잭션 보안을 변경할 수 있습니다. 기본적으로 트랜잭션 보안의 수준은 FULL(동기 운영 모드)로 설정되어 있습니다.  
  
 트랜잭션 보안을 해제하면 세션이 비동기 운영 모드로 바뀌므로 성능이 최대화됩니다. 주 서버를 사용할 수 없는 경우 미러 서버가 중지되지만 웜 대기로 사용할 수 있습니다. 장애 조치(Failover)를 수행하려면 서비스를 강제 적용해야 하며 이 경우 데이터가 손실될 수 있습니다.  
  
### <a name="to-turn-on-transaction-safety"></a>트랜잭션 보안을 설정하려면  
  
1.  주 서버를 연결합니다.  
  
2.  다음 Transact-SQL 문을 실행합니다.  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY FULL  
    ```  
  
     여기서 *\<데이터베이스>* 는 미러된 데이터베이스의 이름입니다.  
  
### <a name="to-turn-off-transaction-safety"></a>트랜잭션 보안을 해제하려면  
  
1.  주 서버를 연결합니다.  
  
2.  다음 문을 실행합니다.  
  
    ```  
    ALTER DATABASE <database> SET PARTNER SAFETY OFF  
    ```  
  
     여기서 *\<데이터베이스>* 는 미러된 데이터베이스입니다.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE 데이터베이스 미러링&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [데이터베이스 미러링 운영 모드](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)  
  
  
