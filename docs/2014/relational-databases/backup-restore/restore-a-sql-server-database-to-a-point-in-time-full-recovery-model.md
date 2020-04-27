---
title: SQL Server 데이터베이스를 지정 시간으로 복원(전체 복구 모델) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- STOPAT clause [RESTORE LOG statement]
- point in time recovery [SQL Server]
- restoring databases [SQL Server], point in time
ms.assetid: 3a5daefd-08a8-4565-b54f-28ad01a47d32
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 66393f8b48c9075c3200b1c56b8447410e143c57
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62921062"
---
# <a name="restore-a-sql-server-database-to-a-point-in-time-full-recovery-model"></a>SQL Server 데이터베이스를 지정 시간으로 복원(전체 복구 모델)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 데이터베이스를 지정 시간으로 복원하는 방법에 대해 설명합니다. 이 항목에서는 전체 또는 대량 로그 복구 모델을 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 관련된 내용을 다룹니다.  
  
> [!IMPORTANT]  
>  대량 로그 복구 모델에서 로그 백업에 대량 로그 변경 내용이 있을 경우 해당 백업 내의 지점으로 지정 시간 복구를 수행할 수 없습니다. 이 경우에는 데이터베이스를 트랜잭션 로그 백업의 끝으로 복구해야 합니다.  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **SQL Server 데이터베이스를 지정 시간으로 복원하려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   STANDBY를 사용하여 알 수 없는 지정 시간을 찾습니다.  
  
-   복원 순서의 이른 시간으로 지정 시간 지정  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 복원할 데이터베이스가 없으면 CREATE DATABASE 권한이 있어야 RESTORE를 실행할 수 있습니다. 데이터베이스가 있으면 RESTORE 권한은 기본적으로 **sysadmin** 및 **dbcreator** 고정 서버 역할의 멤버와 데이터베이스의 소유자(**dbo**)에 설정됩니다. FROM DATABASE_SNAPSHOT 옵션의 경우 데이터베이스가 항상 있습니다.  
  
 멤버 자격 정보를 서버에서 항상 사용할 수 있는 역할에 RESTORE 권한이 제공됩니다. 고정 데이터베이스 역할의 멤버 자격은 데이터베이스가 액세스 가능한 상태이며 손상되지 않은 경우에만 확인할 수 있는데, RESTORE 실행 시 데이터베이스가 항상 이러한 상태인 것은 아니므로 **db_owner** 고정 데이터베이스 역할의 멤버에게는 RESTORE 권한이 없습니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 **데이터베이스를 지정 시간으로 복원하려면**  
  
1.  개체 탐색기에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결하고 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장합니다. 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스**를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **복원**을 가리키고 **데이터베이스**를 클릭합니다.  
  
4.  **일반** 페이지에서 **원본** 섹션을 사용하여 복원할 백업 집합의 원본과 위치를 지정합니다. 다음 옵션 중 하나를 선택합니다.  
  
    -   **Database**  
  
         복원할 데이터베이스를 드롭다운 목록에서 선택합니다. 목록에는 **msdb** 백업 기록에 따라 백업된 데이터베이스만 포함되어 있습니다.  
  
    > [!NOTE]  
    >  백업을 다른 서버에서 가져온 경우 대상 서버에 지정한 데이터베이스에 대한 백업 기록 정보가 없습니다. 이 경우 **디바이스** 를 선택하여 복원할 파일이나 디바이스를 수동으로 지정합니다.  
  
    -   **디바이스**  
  
         찾아보기( **...** ) 단추를 클릭하여 **백업 디바이스 선택** 대화 상자를 엽니다. **백업 미디어 유형** 상자에서 나열된 디바이스 유형 중 하나를 선택합니다. **백업 미디어** 상자에 대해 하나 이상의 디바이스를 선택하려면 **추가**를 클릭합니다.  
  
         원하는 디바이스를 **백업 미디어** 목록 상자에 추가한 후 **확인** 을 클릭하여 **일반** 페이지로 돌아갑니다.  
  
         **원본: 디바이스: 데이터베이스** 목록 상자에서 복원할 데이터베이스의 이름을 선택합니다.  
  
         **참고** 이 목록은 **디바이스** 를 선택한 경우에만 사용할 수 있습니다. 선택한 디바이스에 백업이 있는 데이터베이스만 사용할 수 있습니다.  
  
5.  **대상** 섹션의 **데이터베이스** 상자에는 복원할 데이터베이스의 이름이 자동으로 채워집니다. 데이터베이스의 이름을 변경하려면 **데이터베이스** 상자에 새 이름을 입력합니다.  
  
6.  **일정** 을 클릭하여 **백업 시간대** 대화 상자에 액세스합니다.  
  
7.  **복원 위치** 섹션에서 **특정 날짜 및 시간**을 클릭합니다.  
  
8.  **날짜** 및 **시간** 상자 또는 슬라이더 막대를 사용하여 복원을 중지할 특정 날짜 및 시간을 지정합니다. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  **시간대 간격** 상자를 사용하여 일정에 표시되는 시간을 변경합니다.  
  
9. 특정 지정 시간을 지정한 후에는 데이터베이스 복구 관리자에서 해당 지정 시간에 복원해야 하는 백업만 **복원에 사용할 백업 세트 선택** 표의 **복원** 열에서 선택되도록 합니다. 이러한 선택된 백업은 지정 시간 복원에 필요한 권장 복원 계획을 구성합니다. 지정 시간 복원 작업에는 선택된 백업만을 사용해야 합니다.  
  
     **복원에 사용할 백업 세트** 표의 열에 대한 자세한 내용은 [데이터베이스 복원&#40;일반 페이지&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)을 참조하세요. 데이터베이스 복구 관리자에 대한 자세한 내용은 [복원 및 복구 개요&#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)를 참조하세요.  
  
10. 상황에 따라 **옵션** 페이지의 **복원 옵션** 패널에서 다음 옵션 중 하나를 선택할 수 있습니다.  
  
    -   **기존 데이터베이스 덮어쓰기(WITH REPLACE)**  
  
    -   **복제 설정 유지(WITH KEEP_REPLICATION)**  
  
    -   **복원된 데이터베이스에 대한 액세스 제한(WITH RESTRICTED_USER)**  
  
     이러한 옵션에 대한 자세한 내용은 [데이터베이스 복원&#40;옵션 페이지&#41;](restore-database-options-page.md)을 참조하세요.  
  
11. **복구 상태** 상자에 대한 옵션을 선택합니다. 이 상자에서 복원 작업 후 데이터베이스의 상태를 확인합니다.  
  
    -   **RESTORE WITH RECOVERY** 는 커밋되지 않은 트랜잭션을 롤백하여 데이터베이스를 사용 준비가 된 상태로 유지하는 기본 동작입니다. 추가 트랜잭션 로그를 복원할 수 없습니다. 필요한 모든 백업을 지금 복원하는 경우 이 옵션을 선택합니다.  
  
    -   **RESTORE WITH NORECOVERY** 는 데이터베이스를 비작동 상태로 유지하고 커밋되지 않은 트랜잭션을 롤백하지 않습니다. 추가 트랜잭션 로그를 복원할 수 데이터베이스는 복구할 때까지 사용할 수 없습니다.  
  
    -   **RESTORE WITH STANDBY** 는 읽기 전용 모드로 데이터베이스를 유지합니다. 이 옵션은 커밋되지 않은 트랜잭션의 실행을 취소하지만, 복구 결과를 되돌릴 수 있도록 실행 취소 동작을 대기 파일에 저장합니다.  
  
     옵션에 대한 설명은 [데이터베이스 복원&#40;옵션 페이지&#41;](restore-database-options-page.md)을 참조하세요.  
  
12. **복원 전 비상 로그 백업 수행** 은 선택한 지정 시간에 필요한 경우에 선택됩니다. 이 설정을 수정할 필요는 없지만 필요하지 않은 경우에도 비상 로그를 백업할 수 있습니다.  
  
13. 데이터베이스에 대한 활성 연결이 있으면 복원 작업이 실패할 수 있습니다. **기존 연결 닫기** 옵션을 선택하여 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 와 데이터베이스 간의 모든 활성 연결을 닫습니다. 이 확인란을 선택하면 복원 작업을 수행하기 전에 데이터베이스가 단일 사용자 모드로 설정되고 복원 작업이 완료될 때 데이터베이스가 다중 사용자 모드로 설정됩니다.  
  
14. 각 복원 작업 사이에 확인 메시지를 표시하려면 **각 백업 복원 전에 확인** 을 선택합니다. 데이터베이스가 크고 복원 작업의 상태를 모니터링하려는 경우가 아니면 이 옵션은 일반적으로 필요하지 않습니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 **시작하기 전 주의 사항**  
  
 지정된 시간은 항상 로그 백업에서 복원됩니다. 복원 순서의 모든 RESTORE LOG 문에서 동일한 STOPAT 절에 대상 시간이나 트랜잭션을 지정해야 합니다. 지정 시간 복원을 수행하려면 먼저 종료 지점이 대상 복원 시간보다 빠른 전체 데이터베이스 백업을 복원해야 합니다. 대상 지정 시간이 포함된 로그 백업까지의 모든 후속 로그 백업을 복원하는 동안 이 전체 데이터베이스 백업은 가장 최근 전체 데이터베이스 백업보다 더 오래된 버전일 수 있습니다.  
  
 복원할 데이터베이스를 손쉽게 확인하려면 선택적으로 RESTORE DATABASE 문에 WITH STOPAT 절을 지정하여 데이터 백업이 지정된 대상 시간에 비해 너무 최근인 경우 오류가 발생하도록 하면 됩니다. 그러나 데이터 백업에 대상 시간이 포함된 경우에도 항상 전체 데이터 백업이 복원됩니다.  
  
 **기본 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문**  
  
 <backup_device> STOPAT ** = *`time`*,** RECOVERY로 로그 *database_name* 복원 ...  
  
 복구 지점은 `datetime` *time*에 지정 된 값 또는 그 전에 발생 한 최근 트랜잭션 커밋입니다.  
  
 특정 시점 이전에 수정한 내용만 복원하려면 복원하는 각 백업에 대해 WITH STOPAT **=** *time*을 지정합니다. 이렇게 하면 대상 시간을 지나치지 않게 됩니다.  
  
 **데이터베이스를 지정 시간으로 복원하려면**  
  
> [!NOTE]  
>  이 절차에 대한 예는 이 섹션의 뒷부분에 나오는 [예제(Transact-SQL)](#TsqlExample)을 참조하세요.  
  
1.  데이터베이스를 복원할 서버 인스턴스에 연결합니다.  
  
2.  NORECOVERY 옵션을 사용하여 RESTORE DATABASE 문을 실행합니다.  
  
    > [!NOTE]  
    >  부분 복원 순서에서 [FILESTREAM](../blob/filestream-sql-server.md) 파일 그룹이 제외될 경우 지정 시간 복원은 지원되지 않습니다. 복원 순서를 강제로 계속할 수 있지만 RESTORE 문에서 누락된 FILESTREAM 파일 그룹은 복원되지 않습니다. 지정 시간 복원을 강제로 수행하려면 후속 RESTORE LOG 문에도 지정해야 하는 STOPAT, STOPATMARK 또는 STOPBEFOREMARK 옵션과 함께 CONTINUE_AFTER_ERROR 옵션을 지정합니다. CONTINUE_AFTER_ERROR를 지정하면 부분 복원 순서가 성공하고 FILESTREAM 파일 그룹이 복구 불가능한 상태가 됩니다.  
  
3.  데이터베이스를 복구하지 않고 마지막 전체 데이터베이스 백업과 마지막 차등 데이터베이스 백업(있는 경우)을 복원합니다(RESTORE DATABASE *database_name* FROM *backup_device* WITH NORECOVERY).  
  
4.  로그 복원을 중지할 시간을 지정 하 여 각 트랜잭션 로그 백업을 만들어진 순서 대로 적용 합니다 (<backup_device> STOPAT**=*`time`*,** RECOVERY로 데이터베이스 *database_name* 복원).  
  
    > [!NOTE]  
    >  RECOVERY 및 STOPAT 옵션. 지정된 시간이 트랜잭션 로그에서 수용하는 시간을 초과하는 경우처럼 요청한 시간이 트랜잭션 로그 백업에 포함되지 않을 경우 경고가 생성되고 데이터베이스는 복구되지 않은 상태로 남습니다.  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 `12:00 AM` , `April 15, 2020` 상태로 데이터베이스를 복원하고 여러 로그 백업이 연관된 복원 작업을 보여 줍니다. 백업 디바이스 `AdventureWorksBackups`에서 복원할 전체 데이터베이스 백업은 해당 디바이스의 세 번째 백업 세트(`FILE = 3`)이고, 첫 번째 로그 백업은 네 번째 백업 세트(`FILE = 4`)이고, 두 번째 로그 백업은 다섯 번째 백업 세트(`FILE = 5`)입니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스는 단순 복구 모델을 사용합니다. 로그 백업을 허용하기 위해 전체 데이터베이스를 백업하기 전에 `ALTER DATABASE AdventureWorks SET RECOVERY FULL`을 사용하여 전체 복구 모델을 사용하도록 데이터베이스를 설정했습니다.  
  
```  
RESTORE DATABASE AdventureWorks  
   FROM AdventureWorksBackups  
   WITH FILE=3, NORECOVERY;  
  
RESTORE LOG AdventureWorks  
   FROM AdventureWorksBackups  
   WITH FILE=4, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
  
RESTORE LOG AdventureWorks  
   FROM AdventureWorksBackups  
   WITH FILE=5, NORECOVERY, STOPAT = 'Apr 15, 2020 12:00 AM';  
RESTORE DATABASE AdventureWorks WITH RECOVERY;   
GO  
  
```  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [데이터베이스 백업 복원 &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [전체 복구 모델에서 특정 오류 지점으로 데이터베이스 복원&#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [데이터베이스를 표시된 트랜잭션으로 복원&#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [로그 시퀀스 번호로 복구&#40;SQL Server&#41;](recover-to-a-log-sequence-number-sql-server.md)  
  
## <a name="see-also"></a>참고 항목  
 [backupset &#40;Transact-sql&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [RESTORE HEADERONLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)  
  
  
