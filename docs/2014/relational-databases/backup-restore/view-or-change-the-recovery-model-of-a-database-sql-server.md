---
title: 데이터베이스의 복구 모델 보기 또는 변경(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- database backups [SQL Server], recovery models
- recovery [SQL Server], recovery model
- backing up databases [SQL Server], recovery models
- recovery models [SQL Server], switching
- recovery models [SQL Server], viewing
- database restores [SQL Server], recovery models
- modifying database recovery models
ms.assetid: 94918d1d-7c10-4be7-bf9f-27e00b003a0f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4bc7254d8a3eafa3c7c7d152d323051a3c5bea94
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58537435"
---
# <a name="view-or-change-the-recovery-model-of-a-database-sql-server"></a>데이터베이스 복구 모델 보기 또는 변경
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 데이터베이스의 복구 모델을 보거나 변경하는 방법에 대해 설명합니다. *복구 모델*은 트랜잭션이 로깅되는 방법, 트랜잭션 로그에 백업이 필요하며 허용되는지 여부 및 사용 가능한 복원 작업의 종류를 제어하는 데이터베이스 속성입니다. 사용할 수 있는 복구 모델은 3가지로 단순, 전체 및 대량 로그 복구 모델입니다. 일반적으로 데이터베이스는 전체 복구 모델이나 단순 복구 모델을 사용합니다. 데이터베이스는 언제든지 다른 복구 모델로 전환이 가능합니다. **model** 데이터베이스는 새 데이터베이스의 기본 복구 모델을 설정합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **데이터베이스의 복구 모델 보기 또는 변경 하려면 사용 합니다.**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **후속 권장 사항:**  [복구 모델을 변경한 후](#FollowUp)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   전체 복구 모델 또는 대량 로그 복구 모델에서 전환하기 전에 트랜잭션 로그를 백업합니다.  
  
-   대량 로그 모델에서는 지정 시간 복구를 사용할 수 없습니다. 따라서 트랜잭션 로그 복원이 필요할 수 있는 대량 로그 모델에서 트랜잭션을 실행하는 경우 이러한 트랜잭션이 데이터 손실에 노출될 수 있습니다. 재해 복구 시나리오에서 데이터 복구 기능을 최대화하기 위해 다음 조건에서만 대량 로그 복구 모델로 전환하는 것이 좋습니다.  
  
    -   사용자가 현재 데이터베이스에서 허용되지 않습니다.  
  
    -   대량 프로세스 중 수정된 모든 내용은 로그 백업을 수행하지 않고 대량 프로세스를 다시 실행하는 등의 방법으로 복구할 수 있습니다.  
  
     이러한 두 조건을 충족하면 대량 로그 복구 모델에서 백업된 트랜잭션 로그를 복원하는 동안 데이터 손실에 노출되지 않습니다.  
  
> [!NOTE]  
>  대량 작업 중에 전체 복구 모델로 전환하면 대량 작업의 로깅이 최소 로깅에서 전체 로깅으로 바뀌며 그 반대의 경우도 마찬가지입니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 데이터베이스에 대한 ALTER 권한이 필요합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-or-change-the-recovery-model"></a>복구 모델을 보거나 변경하려면  
  
1.  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스** 를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭하면 **데이터베이스 속성** 대화 상자가 열립니다.  
  
4.  **페이지 선택** 창에서 **옵션**을 클릭합니다.  
  
5.  현재 복구 모델이 **복구 모델** 목록 상자에 표시됩니다.  
  
6.  필요에 따라 복구 모델을 변경하려면 다른 모델 목록을 선택합니다. **전체**, **대량 로그**또는 **단순**을 선택할 수 있습니다.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-view-the-recovery-model"></a>복구 모델을 보려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 [모델](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 데이터베이스의 복구 모델을 배우기 위해 **sys.databases** 카탈로그 뷰를 쿼리하는 방법을 보여줍니다.  
  
```sql  
SELECT name, recovery_model_desc  
   FROM sys.databases  
      WHERE name = 'model' ;  
GO  
  
```  
  
#### <a name="to-change-the-recovery-model"></a>복구 모델을 변경하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 예를 복사하여 쿼리 창에 붙여 넣고 **실행**을 클릭합니다. 이 예에서는 `model` ALTER DATABASE `FULL` 문의 `SET RECOVERY` 옵션을 사용하여 [데이터베이스의 복구 모델을](/sql/t-sql/statements/alter-database-transact-sql-set-options) 로 변경하는 방법을 보여 줍니다.  
  
```sql  
USE master ;  
ALTER DATABASE model SET RECOVERY FULL ;  
```  
  
##  <a name="FollowUp"></a> 후속 권장 사항: 복구 모델을 변경한 후  
  
-   **전체 및 대량 로그 복구 모델 간에 전환한 후**  
  
    -   대량 작업을 완료한 후에는 즉시 전체 복구 모드로 다시 전환하세요.  
  
    -   대량 로그 복구 모델에서 다시 전체 복구 모델로 전환한 후 로그를 백업합니다.  
  
        > [!NOTE]  
        >  백업 전략에 따라 계속해서 주기적인 데이터베이스, 로그 및 차등 백업 작업을 수행합니다.  
  
-   **단순 복구 모델에서 전환한 후**  
  
    -   전체 복구 모델이나 대량 로그 복구 모델로 전환한 후 즉시 전체 또는 차등 데이터베이스 백업을 수행하여 로그 체인을 시작합니다.  
  
        > [!NOTE]  
        >  전체 로그 복구 모델이나 대량 로그 복구 모델로의 전환은 첫 번째 데이터 백업 후에만 적용됩니다.  
  
    -   정기적인 로그 백업을 예약하고 해당 일정에 따라 복원 계획을 업데이트합니다.  
  
        > [!IMPORTANT]  
        >  로그를 자주 백업하지 않으면 트랜잭션 로그가 확장되어 디스크 공간이 부족해질 수 있습니다.  
  
-   **단순 복구 모델로 전환한 후**  
  
    -   트랜잭션 로그 백업에 대한 모든 예약된 작업을 중단합니다.  
  
    -   정기적 데이터베이스 백업이 예약 되어 있는지 확인합니다. 데이터베이스를 백업하는 것은 데이터를 보호하고 트랜잭션 로그의 비활성 부분을 자르는 데 필수적입니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [작업 만들기](../../ssms/agent/create-a-job.md)  
  
-   [작업을 사용하지 않거나 사용하도록 설정](../../ssms/agent/disable-or-enable-a-job.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   [데이터베이스 유지 관리 계획](../maintenance-plans/maintenance-plans.md) ( [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 온라인 설명서)  
  
## <a name="see-also"></a>관련 항목  
 [복구 모델&#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [트랜잭션 로그&#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [sys.databases&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [복구 모델&#40;SQL Server&#41;](recovery-models-sql-server.md)  
  
  
