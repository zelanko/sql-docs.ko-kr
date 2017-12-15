---
title: "데이터베이스 미러링 제거(SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-mirroring
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database mirroring [SQL Server], removing
- removing database mirroring [SQL Server]
ms.assetid: bbc4d7f7-3bc7-40d6-a822-af195fe7f8c0
caps.latest.revision: "42"
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e4557e1e2d52ebc45b73728b813358b07b8bea19
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="remove-database-mirroring-sql-server"></a>데이터베이스 미러링 제거(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 데이터베이스에서 데이터베이스 미러링을 제거하는 방법에 대해 설명합니다.  데이터베이스 소유자는 언제든지 데이터베이스에서 미러링을 제거하여 수동으로 데이터베이스 미러링 세션을 중지할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [보안](#Security)  
  
-   **데이터베이스 미러링을 제거하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [데이터베이스 미러링을 제거한 후](#FollowUp)  
  
-   [관련 태스크](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-remove-database-mirroring"></a>데이터베이스 미러링을 제거하려면  
  
1.  데이터베이스 미러링 세션 중에 주 서버 인스턴스에 연결하고 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 선택한 다음 **미러**를 클릭합니다. **데이터베이스 속성** 대화 상자의 **미러링** 페이지가 열립니다.  
  
4.  **페이지 선택** 창에서 **미러링**을 클릭합니다.  
  
5.  미러링을 제거하려면 **미러링 제거**를 클릭합니다. 확인 메시지가 나타납니다. **예**를 클릭하면 세션이 중지되고 미러링이 데이터베이스에서 제거됩니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 데이터베이스 미러링을 제거하려면 **데이터베이스 속성**을 사용합니다. **데이터베이스 속성** 대화 상자의 **미러링** 페이지를 사용합니다.  
  
#### <a name="to-remove-database-mirroring"></a>데이터베이스 미러링을 제거하려면  
  
1.  한 미러링 파트너의 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행합니다.  
  
    ```  
    ALTER DATABASE database_name SET PARTNER OFF  
    ```  
  
     여기서 *database_name* 은 세션을 제거하려는 미러된 데이터베이스입니다.  
  
     다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 예제 데이터베이스에서 데이터베이스 미러링을 제거합니다.  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET PARTNER OFF;  
    ```  
  
##  <a name="FollowUp"></a> 후속 작업: 데이터베이스 미러링을 제거한 후  
  
> [!NOTE]  
>  미러링 제거의 영향에 대한 자세한 내용은 [데이터베이스 미러링 제거&#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)를 참조하세요.  
  
-   **데이터베이스에서 미러링을 다시 시작하려는 경우**  
  
     미러링이 제거된 후 주 데이터베이스에서 수행된 모든 로그 백업을 미러 데이터베이스에 모두 적용해야만 미러링을 다시 시작할 수 있습니다.  
  
-   **미러링을 다시 시작하지 않으려는 경우**  
  
     필요한 경우 이전 미러 데이터베이스를 복구할 수 있습니다. 미러 서버로 사용했던 서버 인스턴스에 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 사용할 수 있습니다.  
  
    ```  
    RESTORE DATABASE database_name WITH RECOVERY;  
    ```  
  
    > [!IMPORTANT]  
    >  이 데이터베이스를 복구하면 같은 이름의 두 분기 데이터베이스가 온라인 상태가 됩니다. 따라서 클라이언트가 이 두 데이터베이스 중 하나(일반적으로 가장 최근의 주 데이터베이스)에만 액세스할 수 있는지 확인해야 합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [데이터베이스 미러링 세션 일시 중지 또는 재개&#40;SQL Server&#41;](../../database-engine/database-mirroring/pause-or-resume-a-database-mirroring-session-sql-server.md)  
  
-   [데이터베이스 미러링 세션에서 미러링 모니터 서버 제거&#40;SQL Server&#41;](../../database-engine/database-mirroring/remove-the-witness-from-a-database-mirroring-session-sql-server.md)  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 세션 구성&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/database-mirroring-establish-session-windows-authentication.md)  
  
-   [예제: 인증서를 사용하여 데이터베이스 미러링 설정&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/example-setting-up-database-mirroring-using-certificates-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [데이터베이스 미러링 설정&#40;SQL Server&#41;](../../database-engine/database-mirroring/setting-up-database-mirroring-sql-server.md)   
 [Always On 가용성 그룹&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
  
