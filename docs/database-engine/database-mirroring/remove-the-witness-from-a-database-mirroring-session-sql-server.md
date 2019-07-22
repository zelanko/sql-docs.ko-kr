---
title: 데이터베이스 미러링 세션에서 미러링 모니터 서버 제거(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- witness [SQL Server], turning off
- witness [SQL Server], removing
- database mirroring [SQL Server], witness
ms.assetid: f3ce7afc-8936-4d35-80ce-d0f8fbc318d3
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 75a0363d376a16a19fa0c4a07dd0ed2ad0e71fd2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68025274"
---
# <a name="remove-the-witness-from-a-database-mirroring-session-sql-server"></a>데이터베이스 미러링 세션에서 미러링 모니터 서버 제거(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 데이터베이스 미러링 세션에서 미러링 모니터 서버를 제거하는 방법에 대해 설명합니다. 데이터베이스 소유자는 데이터베이스 미러링 세션 중에 언제든지 미러링 모니터를 해제할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **미러링 모니터 서버를 제거하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 작업:**  [미러링 모니터 서버를 제거한 후](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-remove-the-witness"></a>미러링 모니터를 제거하려면  
  
1.  주 서버 인스턴스에 연결한 다음 **개체 탐색기** 창에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장한 다음 미러링 모니터 서버를 제거할 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 선택한 다음 **미러**를 클릭합니다. **데이터베이스 속성** 대화 상자의 **미러링** 페이지가 열립니다.  
  
4.  미러링 모니터 서버를 제거하려면 **미러링 모니터 서버** 필드에서 서버 네트워크 주소를 삭제합니다.  
  
    > [!NOTE]  
    >  자동 장애 조치(failover)가 있는 보호 우선 모드에서 성능 우선 모드로 전환하면 **미러링 모니터 서버** 필드가 자동으로 지워집니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-remove-the-witness"></a>미러링 모니터를 제거하려면  
  
1.  한 파트너 서버 인스턴스의 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 문을 실행합니다.  
  
     [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md) *database_name* SET WITNESS OFF  
  
     여기서 *database_name* 은 미러된 데이터베이스의 이름입니다.  
  
     다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 미러링 모니터 서버를 제거합니다.  
  
    ```  
    ALTER DATABASE AdventureWorks2012 SET WITNESS OFF ;  
    ```  
  
##  <a name="FollowUp"></a> 후속 작업: 미러링 모니터 서버를 제거한 후  
 미러링 모니터 서버를 해제하면 트랜잭션 보안 설정에 따라 [운영 모드](../../database-engine/database-mirroring/database-mirroring-operating-modes.md)가 변경됩니다.  
  
-   트랜잭션 보안을 FULL(기본값)로 설정하면 해당 세션은 자동 장애 조치(Failover)가 없는 보호 우선 동기 모드를 사용합니다.  
  
-   트랜잭션 보안을 OFF로 설정하면 해당 세션은 쿼럼을 필요로 하지 않고 비동기적으로 작동합니다(성능 우선 모드). 트랜잭션 보안을 해제할 때마다 미러링 모니터도 해제하는 것이 좋습니다.  
  
> [!TIP]  
>  각 파트너의 데이터베이스 트랜잭션 보안 설정은 [sys.database_mirroring](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md) 카탈로그 뷰의 **mirroring_safety_level** 및 **mirroring_safety_level_desc** 열에 기록됩니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [Windows 인증을 사용하여 데이터베이스 미러링 모니터 추가&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)  
  
-   [데이터베이스 미러링 모니터 서버 추가 또는 바꾸기&#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/add-or-replace-a-database-mirroring-witness-sql-server-management-studio.md)  
  
## <a name="see-also"></a>참고 항목  
 [ALTER DATABASE 데이터베이스 미러링&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [데이터베이스 미러링 세션에서 트랜잭션 보안 변경&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/change-transaction-safety-in-a-database-mirroring-session-transact-sql.md)   
 [Windows 인증을 사용하여 데이터베이스 미러링 모니터 추가&#40;Transact-SQL&#41;](../../database-engine/database-mirroring/add-a-database-mirroring-witness-using-windows-authentication-transact-sql.md)   
 [데이터베이스 미러링 모니터 서버](../../database-engine/database-mirroring/database-mirroring-witness.md)  
  
  
