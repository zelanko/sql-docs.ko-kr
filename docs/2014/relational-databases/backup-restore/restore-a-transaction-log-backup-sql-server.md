---
title: 트랜잭션 로그 백업 복원(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restoretlog.options.f1
- sql12.swb.restoretlog.general.f1
helpviewer_keywords:
- restore log
- backing up transaction logs [SQL Server], restoring
- transaction log backups [SQL Server], restoring
- restoring transaction logs [SQL Server], restoring backups
- transaction log restores [SQL Server], SQL Server Management Studio
ms.assetid: 1de2b888-78a6-4fb2-a647-ba4bf097caf3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a0cfc68f78ae9ca4022abfb59a33d756e82a6f2f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62875667"
---
# <a name="restore-a-transaction-log-backup-sql-server"></a>트랜잭션 로그 백업 복원(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 트랜잭션 로그 백업을 복원하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [필수 구성 요소](#Prerequisites)  
  
     [보안](#Security)  
  
-   **트랜잭션 로그 백업을 복원하려면:**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   백업은 만든 순서대로 복원해야 합니다. 특정 트랜잭션 로그 백업을 복원하려면 먼저 커밋되지 않은 트랜잭션을 롤백하지 않고, 즉 WITH NORECOVERY로 다음과 같은 이전 백업을 복원해야 합니다.  
  
    -   특정 트랜잭션 로그 백업 이전에 수행된 전체 데이터베이스 백업 및 마지막 차등 백업(있는 경우) 가장 최근의 전체 또는 차등 데이터베이스 백업이 생성되기 전에 데이터베이스에 전체 복구 모델이나 대량 로그 복구 모델이 사용되고 있어야 합니다.  
  
    -   전체 데이터베이스 백업이나 차등 백업 이후(복원하는 경우), 특정 트랜잭션 로그 백업 이전에 수행된 전체 트랜잭션 로그 백업 로그 백업이 로그 체인에 따라 간격 없이 생성된 순서대로 적용되어야 합니다.  
  
         트랜잭션 로그 백업에 대한 자세한 내용은 [트랜잭션 로그 백업&#40;SQL Server&#41;](transaction-log-backups-sql-server.md) 및 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](apply-transaction-log-backups-sql-server.md)을 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 멤버 자격 정보를 서버에서 항상 사용할 수 있는 역할에 RESTORE 권한이 제공됩니다. 고정 데이터베이스 역할의 멤버 자격은 데이터베이스가 액세스 가능한 상태이며 손상되지 않은 경우에만 확인할 수 있는데, RESTORE 실행 시 데이터베이스가 항상 이러한 상태인 것은 아니므로 **db_owner** 고정 데이터베이스 역할의 멤버에게는 RESTORE 권한이 없습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
> [!WARNING]  
>  일반적인 복원 프로세스는 데이터 백업 및 차등 백업과 함께 **데이터베이스 복원** 대화 상자에서 로그 백업을 선택하는 것입니다.  
  
#### <a name="to-restore-a-transaction-log-backup"></a>트랜잭션 로그 백업을 복원하려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스** 를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**, **복원**을 차례로 가리킨 다음 **트랜잭션 로그**를 클릭하여 **트랜잭션 로그 복원** 대화 상자를 엽니다.  
  
    > [!NOTE]  
    >  **트랜잭션 로그** 가 회색으로 표시되어 있는 경우에는 먼저 전체 또는 차등 백업을 복원해야 할 수 있습니다. **데이터베이스 백업** 대화 상자를 사용하세요.  
  
4.  **일반** 페이지의 **데이터베이스** 목록 상자에서 데이터베이스의 이름을 선택합니다. 복원 중인 상태의 데이터베이스만 나열됩니다.  
  
5.  복원할 백업 세트의 원본 및 위치를 지정하려면 다음 옵션 중 하나를 클릭합니다.  
  
    -   **데이터베이스의 이전 백업 원본**  
  
         복원할 데이터베이스를 드롭다운 목록에서 선택합니다. 목록에는 **msdb** 백업 기록에 따라 백업된 데이터베이스만 포함되어 있습니다.  
  
    -   **파일 또는 테이프 원본**  
  
         찾아보기( **...** ) 단추를 클릭하여 **백업 디바이스 선택** 대화 상자를 엽니다. **백업 미디어 유형** 상자에서 나열된 장치 유형 중 하나를 선택합니다. **백업 미디어** 상자에 대해 하나 이상의 장치를 선택하려면 **추가**를 클릭합니다.  
  
         원하는 디바이스를 **백업 미디어** 목록 상자에 추가한 후 **확인** 을 클릭하여 **일반** 페이지로 돌아갑니다.  
  
6.  **복원할 트랜잭션 로그 백업 선택** 표에서 복원할 백업을 선택합니다. 이 표에는 선택한 데이터베이스에 사용할 수 있는 트랜잭션 로그 백업이 나열됩니다. 로그 백업은 **첫 번째 LSN** 이 데이터베이스의 **마지막 LSN** 보다 큰 경우에만 사용할 수 있습니다. 로그 백업은 포함된 LSN(로그 시퀀스 번호) 순서로 나열되며 이 순서로 복원되어야 합니다.  
  
     다음 표에서는 표의 열 머리글을 나열하고 해당 값을 설명합니다.  
  
    |헤더|값|  
    |------------|-----------|  
    |**복원**|선택된 확인란은 복원될 백업 세트를 나타냅니다.|  
    |**이름**|백업 세트의 이름입니다.|  
    |**구성 요소**|백업 된 구성 요소: **데이터베이스**하십시오 **파일**, 또는 \<빈 > (트랜잭션 로그의 경우)에 대 한 합니다.|  
    |**데이터베이스 백업**|백업 작업과 연관된 데이터베이스의 이름입니다.|  
    |**Start Date**|클라이언트의 국가별 설정으로 표시되는 백업 작업 시작 날짜 및 시간입니다.|  
    |**완료 날짜**|클라이언트의 국가별 설정으로 표시되는 백업 작업 완료 날짜 및 시간입니다.|  
    |**첫 번째 LSN**|백업 세트에 있는 첫 번째 트랜잭션의 로그 시퀀스 번호입니다. 파일 백업의 경우 비워 둡니다.|  
    |**마지막 LSN**|백업 세트에 있는 마지막 트랜잭션의 로그 시퀀스 번호입니다. 파일 백업의 경우 비워 둡니다.|  
    |**검사점 LSN**|백업 생성 시 가장 최근 검사점의 로그 시퀀스 번호|  
    |**전체 LSN**|가장 최근 전체 데이터베이스 백업의 로그 시퀀스 번호입니다.|  
    |**Server**|백업 작업을 수행한 데이터베이스 엔진 인스턴스의 이름입니다.|  
    |**사용자 이름**|백업 작업을 수행한 사용자의 이름입니다.|  
    |**크기**|백업 세트의 크기(바이트)입니다.|  
    |**위치**|볼륨에 있는 백업 세트의 위치입니다.|  
    |**만료**|백업 세트가 만료되는 날짜 및 시간입니다.|  
  
7.  다음 중 하나를 선택합니다.  
  
    -   **지정 시간**  
  
         기본값(**가장 최근**)을 유지하거나 찾아보기 단추를 클릭하여 표시된 **특정 시점 복원** 대화 상자에서 특정 날짜 및 시간을 선택합니다.  
  
    -   **표시된 트랜잭션**  
  
         데이터베이스를 이전에 표시된 트랜잭션으로 복원합니다. 이 옵션을 선택하면 **표시된 트랜잭션** 대화 상자가 시작됩니다. 이 대화 상자에는 선택한 트랜잭션 로그 백업에 사용할 수 있는 표시된 트랜잭션이 나열된 표가 나타납니다.  
  
         기본적으로 표시된 트랜잭션 이전까지만 복원합니다. 표시된 트랜잭션도 복원하려면 **표시된 트랜잭션 포함**을 선택합니다.  
  
         다음 표에서는 표의 열 머리글을 나열하고 해당 값을 설명합니다.  
  
        |헤더|값|  
        |------------|-----------|  
        |\<비어 있음>|표시 선택을 위한 확인란을 표시합니다.|  
        |**트랜잭션 표시**|트랜잭션이 커밋될 때 사용자가 지정한 표시된 트랜잭션의 이름입니다.|  
        |**날짜**|트랜잭션이 커밋된 날짜 및 시간입니다. 트랜잭션 날짜 및 시간은 클라이언트 컴퓨터의 날짜 및 시간이 아닌 **msdbgmarkhistory** 테이블에 기록된 날짜 및 시간으로 표시됩니다.|  
        |**설명**|트랜잭션이 커밋될 때 사용자가 지정한 표시된 트랜잭션에 대한 설명입니다(있는 경우).|  
        |**LSN**|표시된 트랜잭션의 로그 시퀀스 번호입니다.|  
        |**데이터베이스 백업**|표시된 트랜잭션이 커밋된 데이터베이스의 이름입니다.|  
        |**사용자 이름**|표시된 트랜잭션을 커밋한 데이터베이스 사용자의 이름입니다.|  
  
8.  고급 옵션을 보거나 선택하려면 **페이지 선택** 창에서 **옵션** 을 클릭합니다.  
  
9. **복원 옵션** 섹션에서 선택 항목은 다음과 같습니다.  
  
    -   **복제 설정 유지(WITH KEEP_REPLICATION)**  
  
         게시된 데이터베이스를 해당 데이터베이스가 생성된 서버 이외의 다른 서버로 복원할 경우 복제 설정을 유지합니다.  
  
         이 옵션은만 사용할 수는 **커밋되지 않은 트랜잭션을 롤백하여 데이터베이스를 사용할 수 있도록 유지 하는 중...**  해당 백업을 복원 하는 옵션 (뒷부분에서 설명)과 `RECOVERY` 옵션입니다.  
  
         사용 하는이 옵션을 선택 합니다 `KEEP_REPLICATION` 옵션을 [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE` 문입니다.  
  
    -   **각 백업 복원 전에 확인**  
  
         첫 번째 복원 후 각 백업 세트를 복원하기 전에 이 옵션은 복원 시퀀스를 계속할지 여부를 묻는 **복원 계속** 대화 상자를 표시합니다. 이 대화 상자는 다음 미디어 세트(사용 가능한 경우)의 이름, 백업 세트 이름 및 백업 세트 설명을 표시합니다.  
  
         이 옵션은 다양한 미디어 세트의 테이프를 바꿔야 할 때 특히 유용합니다. 예를 들어 서버에 한 개의 테이프 디바이스만 있을 때 이 옵션을 사용할 수 있습니다. **확인**을 클릭하기 전에 진행할 준비가 될 때까지 기다리세요.  
  
         **아니요** 를 클릭하면 데이터베이스를 복원 중인 상태로 둡니다. 사용자 편의를 위해 완료된 마지막 복원 다음에 복원 시퀀스를 계속할 수 있습니다. 다음 백업이 데이터 백업 또는 차등 백업인 경우 **데이터베이스 복원** 태스크를 다시 사용하세요. 다음 백업이 로그 백업인 경우 **트랜잭션 로그 복원** 태스크를 사용합니다.  
  
    -   **복원된 데이터베이스에 대한 액세스 제한(WITH RESTRICTED_USER)**  
  
         **db_owner**, **dbcreator**또는 **sysadmin**의 멤버만 복원된 데이터베이스를 사용할 수 있도록 합니다.  
  
         사용 하 여 동의어는이 옵션을 선택 합니다 `RESTRICTED_USER` 옵션을 [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE` 문입니다.  
  
10. **복구 상태** 옵션에서 복원 작업 이후의 데이터베이스 상태를 지정합니다.  
  
    -   **커밋되지 않은 트랜잭션을 롤백하여 데이터베이스를 사용할 수 있는 상태로 유지합니다. 추가 트랜잭션 로그를 복원할 수 없습니다. (RESTORE WITH RECOVERY)**  
  
         데이터베이스를 복구합니다. 이 옵션은 해당 하는 `RECOVERY` 옵션을 [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE` 문입니다.  
  
         복원할 로그 파일이 없는 경우에만 이 옵션을 선택합니다.  
  
    -   **데이터베이스를 비작동 상태로 유지하고 커밋되지 않은 트랜잭션을 롤백하지 않습니다. 추가 트랜잭션 로그를 복원할 수 (RESTORE WITH NORECOVERY)**  
  
         데이터베이스를 복원되지 않은 `RESTORING` 상태로 유지합니다. 이 옵션을 사용 하는 `NORECOVERY` 옵션을 [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE` 문입니다.  
  
         이 옵션을 선택하면 **복제 설정 유지** 옵션을 사용할 수 없습니다.  
  
        > [!IMPORTANT]  
        >  미러 또는 보조 데이터베이스의 경우 항상 이 옵션을 선택합니다.  
  
    -   **데이터베이스를 읽기 전용 모드로 유지합니다. 커밋되지 않은 트랜잭션 실행을 취소하지만 복구 결과를 되돌릴 수 있도록 실행 취소 동작을 파일에 (RESTORE WITH STANDBY)**  
  
         데이터베이스를 대기 모드로 유지합니다. 이 옵션을 사용 하는 `STANDBY` 옵션을 [!INCLUDE[tsql](../../includes/tsql-md.md)] `RESTORE` 문입니다.  
  
         이 옵션을 선택하려면 대기 파일을 지정해야 합니다.  
  
11. 필요에 따라 **대기 파일** 입력란에 대기 파일 이름을 지정합니다. 데이터베이스를 읽기 전용 모드로 유지하는 경우 이 옵션이 필요합니다. 대기 파일을 찾아보거나 입력란에 해당 경로 이름을 입력할 수 있습니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
> [!IMPORTANT]  
>  모호하지 않도록 항상 모든 RESTORE 문에 명시적으로 WITH NORECOVERY 또는 WITH RECOVERY를 지정하는 것이 좋습니다. 이는 스크립트 작성 시 특히 중요합니다.  
  
#### <a name="to-restore-a-transaction-log-backup"></a>트랜잭션 로그 백업을 복원하려면  
  
1.  RESTORE LOG 문을 실행하여 트랜잭션 로그 백업을 적용합니다. 이때 다음을 지정합니다.  
  
    -   트랜잭션 로그가 적용될 데이터베이스의 이름  
  
    -   트랜잭션 로그 백업이 복원될 백업 디바이스  
  
    -   NORECOVERY 절  
  
     이 문의 기본 구문은 다음과 같습니다.  
  
     RESTORE LOG *database_name* FROM <backup_device> WITH NORECOVERY.  
  
     여기서 *database_name*은 데이터베이스의 이름이고 <backup_device>는 복원 중인 로그 백업이 포함된 장치의 이름입니다.  
  
2.  적용해야 할 각 트랜잭션 로그 백업에 대해 1단계를 반복합니다.  
  
3.  복원 시퀀스의 마지막 백업을 복원한 후 데이터베이스를 복구하려면 다음 문 중 하나를 사용합니다.  
  
    -   데이터베이스를 마지막 RESTORE LOG 문의 일부로 복구합니다.  
  
        ```  
        RESTORE LOG <database_name> FROM <backup_device> WITH RECOVERY;  
        GO  
        ```  
  
    -   별도의 RESTORE DATABASE 문을 사용하여 데이터베이스를 복구할 때까지 기다립니다.  
  
        ```  
        RESTORE LOG <database_name> FROM <backup_device> WITH NORECOVERY;   
        RESTORE DATABASE <database_name> WITH RECOVERY;  
        GO  
        ```  
  
         데이터베이스를 복구할 때까지 기다리면 필요한 모든 로그 백업을 복원했는지 확인할 수 있습니다. 이 방법은 지정 시간 복원을 수행할 때 사용하는 것이 좋습니다.  
  
    > [!IMPORTANT]  
    >  미러 데이터베이스를 만드는 경우 복구 단계를 생략하세요. 미러 데이터베이스는 RESTORING 상태로 유지되어야 합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 기본적으로 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스는 단순 복구 모델을 사용합니다. 다음 예에서는 전체 복구 모델을 사용하도록 데이터베이스를 다음과 같이 변경해야 합니다.  
  
```sql  
ALTER DATABASE AdventureWorks2012 SET RECOVERY FULL;  
```  
  
#### <a name="a-applying-a-single-transaction-log-backup"></a>1\. 단일 트랜잭션 로그 백업 적용  
 다음 예에서는 먼저 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 이라는 백업 디바이스에 상주하는 전체 데이터베이스 백업을 사용하여 `AdventureWorks2012_1`데이터베이스를 복원합니다. 그런 다음 `AdventureWorks2012_log`라는 백업 디바이스에 상주하는 첫 번째 트랜잭션 로그 백업을 적용합니다. 마지막으로 데이터베이스를 복구합니다.  
  
```sql  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorks2012_1  
   WITH NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 1,  
   WITH NORECOVERY;  
GO  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY;  
GO  
```  
  
#### <a name="b-applying-multiple-transaction-log-backups"></a>2\. 여러 트랜잭션 로그 백업 적용  
 다음 예에서는 먼저 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 이라는 백업 디바이스에 상주하는 전체 데이터베이스 백업을 사용하여 `AdventureWorks2012_1`데이터베이스를 복원합니다. 그런 다음 `AdventureWorks2012_log`라는 백업 디바이스에 상주하는 처음 3개의 트랜잭션 로그 백업을 하나씩 적용합니다. 마지막으로 데이터베이스를 복구합니다.  
  
```sql  
RESTORE DATABASE AdventureWorks2012  
   FROM AdventureWorks2012_1  
   WITH NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 1,  
   NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 2,  
   WITH NORECOVERY;  
GO  
RESTORE LOG AdventureWorks2012  
   FROM AdventureWorks2012_log  
   WITH FILE = 3,  
   WITH NORECOVERY;  
GO  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY;  
GO  
```  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [데이터베이스 백업 복원 &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [전체 복구 모델에서 특정 오류 지점으로 데이터베이스 복원&#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
-   [데이터베이스를 표시된 트랜잭션으로 복원&#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
## <a name="see-also"></a>관련 항목  
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](apply-transaction-log-backups-sql-server.md)  
  
  
