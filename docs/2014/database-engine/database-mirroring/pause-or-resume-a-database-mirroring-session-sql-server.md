---
title: 데이터베이스 미러링 세션 일시 중지 또는 재개(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- resuming database mirroring
- database mirroring [SQL Server], sessions
- database mirroring [SQL Server], pausing
- database mirroring [SQL Server], resuming
- pausing database mirroring
ms.assetid: 05ede3b4-6abe-4442-abb7-9f5aee1d6bc0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 52781de1cd4b6309f3ebeb9a2c59ae85b0b32dbd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62754592"
---
# <a name="pause-or-resume-a-database-mirroring-session-sql-server"></a>데이터베이스 미러링 세션 일시 중지 또는 재개(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 데이터베이스 미러링을 일시 중지하거나 재개하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **ReplaceThisText으로 다음을 사용 합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [데이터베이스 미러링을 일시 중지 하거나 재개 한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
 언제든지 데이터베이스 미러링 세션을 일시 중지하여 병목 상태에서 성능을 향상시킬 수 있으며, 일시 중지된 세션을 언제든지 재개할 수 있습니다.  
  
> [!CAUTION]  
>  강제 서비스 이후에 원래 주 서버가 다시 연결되면 미러링이 일시 중지됩니다. 이 경우 미러링을 재개하면 원래 주 서버의 데이터가 손실될 수 있습니다. 데이터 손실 위험을 관리하는 방법은 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)을 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 데이터베이스 미러링 세션을 일시 중지하거나 재개하려면 **데이터베이스 속성 미러링** 페이지를 사용하세요.  
  
#### <a name="to-pause-or-resume-database-mirroring"></a>데이터베이스 미러링을 일시 중지 또는 재개하려면  
  
1.  데이터베이스 미러링 세션 중에 주 서버 인스턴스에 연결하고 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  
  **데이터베이스**를 확장하고 해당 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 선택한 다음 **미러**를 클릭합니다. **데이터베이스 속성** 대화 상자의 **미러링** 페이지가 열립니다.  
  
4.  세션을 일시 중지하려면 **일시 중지**를 클릭합니다.  
  
     확인 메시지가 나타납니다. **예**를 클릭하면 세션이 일시 중지되고 단추가 **재개**로 바뀝니다.  
  
     세션의 일시 중지에 따른 영향에 대한 자세한 내용은 [데이터베이스 미러링 일시 중지 및 재개&#40;SQL Server&#41;](database-mirroring-sql-server.md)를 참조하세요.  
  
5.  세션을 재개하려면 **재개**를 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-pause-database-mirroring"></a>데이터베이스 미러링을 일시 중지하려면  
  
1.  한 파트너에 대한 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
     ALTER DATABASE *database_name* SET PARTNER SUSPEND  
  
     여기서 *database_name* 은 일시 중지할 세션이 있는 미러된 데이터베이스입니다.  
  
     다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스를 일시 중지합니다.  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER SUSPEND;  
    ```  
  
##### <a name="to-resume-database-mirroring"></a>데이터베이스 미러링을 재개하려면  
  
1.  한 파트너에 대한 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 Transact-SQL 문을 실행합니다.  
  
     ALTER DATABASE *database_name* SET PARTNER RESUME  
  
     여기서 *database_name* 은 세션을 재개하려는 미러된 데이터베이스입니다.  
  
     다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스를 일시 중지합니다.  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER RESUME;  
    ```  
  
##  <a name="FollowUp"></a>후속 작업: 데이터베이스 미러링을 일시 중지 하거나 재개 한 후  
  
-   **데이터베이스 미러링을 일시 중지 한 후**  
  
     주 데이터베이스에서 전체 트랜잭션 로그를 피하기 위해 예방 조치를 취해야 합니다. 자세한 내용은 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)을(를) 참조하세요.  
  
-   **데이터베이스 미러링을 재개 한 후**  
  
     데이터베이스 미러링을 재개하면 미러 데이터베이스는 SYNCHRONIZING 상태가 됩니다. 보안 수준이 FULL인 경우 미러 데이터베이스는 주 데이터베이스와 동기화되고 SYNCHRONIZED 상태가 됩니다. 이 시점에서 장애 조치(Failover)가 가능합니다. 미러링 모니터가 있고 ON 상태인 경우 자동 장애 조치가 가능합니다. 미러링 모니터가 없는 경우 수동 장애 조치가 가능합니다.  
  
##  <a name="RelatedTasks"></a> 관련 작업  
  
-   [데이터베이스 미러링 제거&#40;SQL Server&#41;](remove-database-mirroring-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링&#40;SQL Server&#41;](database-mirroring-sql-server.md)  
  
  
