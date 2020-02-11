---
title: 페이지 복원(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restorepage.general.f1
helpviewer_keywords:
- restoring pages [SQL Server]
- pages [SQL Server], restoring
- databases [SQL Server], damaged
- page restores [SQL Server]
- pages [SQL Server], damaged
- restoring [SQL Server], pages
ms.assetid: 07e40950-384e-4d84-9ac5-84da6dd27a91
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f45fe94756ffa30a458aabbb078f6b01c9821918
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62921035"
---
# <a name="restore-pages-sql-server"></a>페이지 복원(SQL Server)
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 페이지를 복원하는 방법에 대해 설명합니다. 페이지 복원의 목표는 전체 데이터베이스를 복원하지 않고 하나 이상의 손상된 페이지를 복원하는 것입니다. 일반적으로 복원 후보 페이지는 페이지에 액세스할 때 발생한 오류 때문에 "주의 대상"으로 표시됩니다. 주의 대상 페이지는 [msdb](/sql/relational-databases/system-tables/suspect-pages-transact-sql) 데이터베이스의 **suspect_pages** 테이블에서 확인할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [페이지 복원이 유용한 경우](#WhenUseful)  
  
     [제한 사항](#Restrictions)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **페이지를 복원하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="WhenUseful"></a> 페이지 복원이 유용한 경우  
 페이지 복원은 격리된 손상 페이지를 복구하기 위한 기능입니다. 몇몇 페이지를 각각 복원하고 복구하면 복원 작업 도중 오프라인 상태인 데이터의 양이 줄어들어 파일 복원보다 빠를 수 있습니다. 그러나 파일에 있는 여러 페이지를 복원할 경우에는 일반적으로 전체 파일을 복원하는 것이 효율적입니다. 예를 들어 디바이스의 여러 페이지에서 디바이스 오류의 가능성을 나타내는 경우 파일을 다른 위치로 복원한 다음 해당 디바이스를 복구해 보세요.  
  
 또한 모든 페이지 오류를 복원해야 하는 것은 아닙니다. 보조 인덱스와 같은 캐시 데이터에서 발생한 문제는 데이터를 다시 계산하여 해결할 수 있습니다. 예를 들어 데이터베이스 관리자가 보조 인덱스를 삭제하고 다시 작성하면 손상된 데이터는 수정되었더라도 [suspect_pages](/sql/relational-databases/system-tables/suspect-pages-transact-sql) 테이블에 이러한 수정 내용이 반영되지 않습니다.  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   페이지 복원은 전체 복구 모델 또는 대량 로그 복구 모델을 사용하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 적용됩니다. 페이지 복원은 읽기/쓰기 파일 그룹에 대해서만 지원됩니다.  
  
-   데이터베이스 페이지만 복원할 수 있습니다. 다음 항목은 페이지 복원을 사용하여 복원할 수 없습니다.  
  
    -   트랜잭션 로그  
  
    -   할당 페이지: GAM(전역 할당 맵) 페이지, SGAM(공유 전역 할당 맵) 페이지 및 PFS(페이지 여유 공간) 페이지.  
  
    -   모든 데이터 파일의 0페이지(파일 부트 페이지)  
  
    -   1:9페이지(데이터베이스 부트 페이지)  
  
    -   전체 텍스트 카탈로그  
  
-   대량 로그 복구 모델을 사용하는 데이터베이스의 경우 페이지 복원에는 다음의 추가 조건이 있습니다.  
  
    -   파일 그룹 또는 페이지 데이터가 오프라인 상태인 동안 백업하는 것은 오프라인 데이터가 로그에 기록되지 않으므로 대량 로그 데이터의 경우 문제가 될 수 있습니다. 오프라인 페이지가 있으면 로그를 백업하지 못할 수 있습니다. 이 경우 가장 최근의 백업으로 복원하는 것보다 데이터가 적게 손실될 수 있으므로 DBCC REPAIR를 사용하세요.  
  
    -   대량 로그 데이터베이스의 로그 백업에서 잘못된 페이지가 나타나면 WITH CONTINUE_AFTER_ERROR가 지정되지 않는 경우 로그 백업은 실패합니다.  
  
    -   일반적으로 페이지 복원은 대량 로그 복구에서 작동하지 않습니다.  
  
         페이지 복원을 수행하는 최선의 구현 방법은 데이터베이스를 전체 복구 모델로 설정하고 로그 백업을 시도하는 것입니다. 로그 백업이 성공하면 페이지 복원을 계속 진행할 수 있습니다. 로그 백업이 실패하면 이전 로그 백업 이후의 작업을 잃게 되거나 REPAIR_ALLOW_DATA_LOSS 옵션을 사용하여 DBCC를 실행해야 합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   페이지 복원 시나리오:  
  
     오프라인 페이지 복원  
     모든 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 데이터베이스가 오프라인 상태일 때에도 페이지를 복원할 수 있습니다. 오프라인 페이지 복원에서 손상된 페이지가 복원되는 동안 데이터베이스는 오프라인 상태가 됩니다. 복원 시퀀스의 마지막에 데이터베이스는 온라인 상태가 됩니다.  
  
     온라인 페이지 복원  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition에서는 온라인 페이지 복원을 지원하며, 데이터베이스가 현재 오프라인 상태인 경우에는 오프라인 복원을 사용합니다. 대부분의 경우 손상된 페이지는 페이지가 복원될 파일 그룹을 비롯한 데이터베이스가 온라인 상태로 유지되는 동안 복원될 수 있습니다. 주 파일 그룹이 온라인 상태이면 하나 이상의 보조 파일 그룹이 오프라인 상태이더라도 페이지 복원은 대개 온라인 상태로 수행됩니다. 그러나 손상된 페이지를 오프라인으로 복원해야 하는 경우도 있습니다. 예를 들어 중요한 특정 페이지가 손상되어 데이터베이스를 시작할 수 없는 경우가 이에 해당합니다.  
  
    > [!WARNING]  
    >  손상된 페이지에 중요한 데이터베이스 메타데이터가 저장되어 있으면 온라인 페이지 복원을 시도하는 동안 메타데이터에 필요한 업데이트가 실패할 수 있습니다. 이 경우 오프라인 페이지 복원을 수행할 수 있지만 이를 위해서는 먼저 RESTORE WITH NORECOVERY로 트랜잭션 로그를 백업하여 [비상 로그 백업](tail-log-backups-sql-server.md) 을 만들어야 합니다.  
  
-   페이지 복원은 페이지 체크섬을 포함하여 향상된 페이지 수준 오류 보고와 추적을 사용합니다. 페이지가 체크섬이나 조각난 쓰기에 의해 손상된 것으로 확인될 경우 이러한 *손상된 페이지*는 페이지 복원 작업을 통해 복원할 수 있습니다. 이때 명시적으로 지정한 페이지만 복원됩니다. 지정한 각 페이지는 지정한 데이터 백업의 해당 페이지 복사본으로 대체됩니다.  
  
     후속 로그 백업을 복원하는 경우 복구할 페이지가 하나 이상 포함된 데이터베이스 파일에만 백업이 적용됩니다. 해당 페이지를 포함하는 파일 그룹을 현재 로그 파일로 가져오려면 손상되지 않은 로그 백업 체인을 마지막 전체 복원 또는 차등 복원에 적용해야 합니다. 파일 복원의 경우와 같이 롤포워드 세트는 단일 로그 다시 실행 과정을 사용하여 진행됩니다. 페이지 복원이 성공하기 위해서는 복원된 페이지가 데이터베이스와 동일한 상태로 복구되어야 합니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 복원할 데이터베이스가 없으면 CREATE DATABASE 권한이 있어야 RESTORE를 실행할 수 있습니다. 데이터베이스가 있으면 RESTORE 권한은 기본적으로 **sysadmin** 및 **dbcreator** 고정 서버 역할의 멤버와 데이터베이스의 소유자(**dbo**)에 설정됩니다. FROM DATABASE_SNAPSHOT 옵션의 경우 데이터베이스가 항상 있습니다.  
  
 멤버 자격 정보를 서버에서 항상 사용할 수 있는 역할에 RESTORE 권한이 제공됩니다. 고정 데이터베이스 역할의 멤버 자격은 데이터베이스가 액세스 가능한 상태이며 손상되지 않은 경우에만 확인할 수 있는데, RESTORE 실행 시 데이터베이스가 항상 이러한 상태인 것은 아니므로 **db_owner** 고정 데이터베이스 역할의 멤버에게는 RESTORE 권한이 없습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]부터는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 페이지 복원을 지원합니다.  
  
#### <a name="to-restore-pages"></a>페이지를 복원하려면  
  
1.  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결하고 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장합니다. 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스**를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**, **복원**을 차례로 가리킨 다음 **페이지**를 클릭하여 **페이지 복원** 대화 상자를 엽니다.  
  
     **복원**  
     이 섹션은 **데이터베이스 복원(일반 페이지)** 의 [복원 위치](../../integration-services/general-page-of-integration-services-designers-options.md)와 동일한 기능을 수행합니다.  
  
     **Database**  
     복원할 데이터베이스를 지정합니다. 새 데이터베이스를 입력하거나 드롭다운 목록에서 기존 데이터베이스를 선택할 수 있습니다. 이 목록에는 시스템 데이터베이스인 **master** 및 **tempdb**를 제외한 서버의 모든 데이터베이스가 포함되어 있습니다.  
  
    > [!WARNING]  
    >  암호로 보호된 백업을 복원하려면 [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 문을 사용해야 합니다.  
  
     **비상 로그 백업**  
     **백업 디바이스** 에서 데이터베이스에 대한 비상 로그 백업이 저장될 파일 이름을 입력하거나 선택합니다.  
  
     **백업 세트**  
     이 섹션에는 복원에 관련된 백업 세트가 표시됩니다.  
  
    |헤더|값|  
    |------------|------------|  
    |**이름**|백업 세트의 이름입니다.|  
    |**구성 요소**|백업된 구성 요소: **데이터베이스**, **파일** 또는 **\<비어 있음>** (트랜잭션 로그의 경우)이 될 수 있습니다.|  
    |**형식**|수행된 백업 유형입니다. **전체**, **차등**또는 **트랜잭션 로그**일 수 있습니다.|  
    |**Server**|백업 작업을 수행한 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스의 이름입니다.|  
    |**Database**|백업 작업과 관련된 데이터베이스의 이름입니다.|  
    |**위치**|볼륨에 있는 백업 세트의 위치입니다.|  
    |**첫 번째 LSN**|백업 세트에 있는 첫 번째 트랜잭션의 LSN(로그 시퀀스 번호)입니다. 파일 백업의 경우 비워 둡니다.|  
    |**마지막 LSN**|백업 세트에 있는 마지막 트랜잭션의 LSN(로그 시퀀스 번호)입니다. 파일 백업의 경우 비워 둡니다.|  
    |**검사점 LSN**|백업을 만들 때 가장 최근 검사점의 로그 시퀀스 번호입니다.|  
    |**전체 LSN**|가장 최근에 수행한 전체 데이터베이스 백업의 LSN(로그 시퀀스 번호)입니다.|  
    |**Start Date**|클라이언트의 국가별 설정으로 표시되는 백업 작업 시작 날짜 및 시간입니다.|  
    |**완료 날짜**|클라이언트의 국가별 설정으로 표시되는 백업 작업 완료 날짜 및 시간입니다.|  
    |**크기**|백업 세트의 크기를 바이트 단위로 표시한 것입니다.|  
    |**사용자 이름**|백업 작업을 수행한 사용자의 이름입니다.|  
    |**만료**|백업 세트가 만료되는 날짜 및 시간입니다.|  
  
     페이지 복원 작업을 수행하는 데 필요한 백업 파일의 무결성을 확인하려면 **확인** 을 클릭합니다.  
  
4.  손상된 페이지를 확인하려면 **데이터베이스** 상자에서 올바른 데이터베이스를 선택한 상태에서 **데이터베이스 페이지 확인**을 클릭합니다. 이 작업을 실행하는 데는 오랜 시간이 소요됩니다.  
  
    > [!WARNING]  
    >  손상되지 않은 특정 페이지를 복원하려면 **추가** 를 클릭하고 복원할 페이지의 **파일 ID** 와 **페이지 ID** 를 입력합니다.  
  
5.  복원할 페이지를 확인하는 데는 페이지 표가 사용됩니다. 처음에는 이 표가 [suspect_pages](/sql/relational-databases/system-tables/suspect-pages-transact-sql) 시스템 테이블의 내용으로 채워집니다. 표에서 페이지를 추가하거나 제거하려면 **추가** 또는 **제거**를 클릭합니다. 자세한 내용은 [suspect_pages 테이블 관리&#40;SQL Server&#41;](manage-the-suspect-pages-table-sql-server.md)에서 페이지를 복원하는 방법에 대해 설명합니다.  
  
6.  **백업 세트** 표에는 기본 복원 계획의 백업 세트가 나열됩니다. 필요할 경우 **확인** 을 클릭하여 복원은 수행하지 않고 백업을 읽을 수 있는지와 백업 세트가 완전한지만 확인할 수 있습니다. 자세한 내용은 [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)를 참조하세요.  
  
     **페이지**  
  
7.  페이지 표에 나열된 페이지를 복원하려면 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 RESTORE DATABASE 문에서 페이지를 지정하려면 페이지를 포함하는 파일의 파일 ID와 해당 페이지의 페이지 ID가 필요합니다. 필요한 구문은 다음과 같습니다.  
  
 `RESTORE DATABASE <database_name>`  
  
 `PAGE = '<file: page> [ ,... n ] ' [ ,... n ]`  
  
 `FROM <backup_device> [ ,... n ]`  
  
 `WITH NORECOVERY`  
  
 PAGE 옵션의 매개 변수에 대한 자세한 내용은 [RESTORE 인수&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-arguments-transact-sql)를 참조하세요. RESTORE DATABASE 구문에 대한 자세한 내용은 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)를 참조하세요.  
  
#### <a name="to-restore-pages"></a>페이지를 복원하려면  
  
1.  복원하려는 손상된 페이지의 페이지 ID를 확인합니다. 체크섬 또는 조각난 쓰기 오류가 페이지 ID를 반환하고 페이지를 지정하는 데 필요한 정보를 제공합니다. 손상된 페이지의 페이지 ID를 조회하려면 다음 원본 중 하나를 사용하세요.  
  
    |페이지 ID의 원본|항목|  
    |-----------------------|-----------|  
    |**msdb..suspect_pages**|[suspect_pages 테이블 관리&#40;SQL Server&#41;](manage-the-suspect-pages-table-sql-server.md)|  
    |오류 로그|[SQL Server 오류 로그 보기&#40;SQL Server Management Studio&#41;](../../ssms/sql-server-management-studio-ssms.md)|  
    |이벤트 추적|[이벤트 모니터링 및 응답](../../ssms/agent/monitor-and-respond-to-events.md)|  
    |DBCC|[DBCC&#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-transact-sql)|  
    |WMI 공급자|[서버 이벤트용 WMI 공급자 개념](../wmi-provider-server-events/wmi-provider-for-server-events-concepts.md)|  
  
2.  페이지가 들어 있는 전체 데이터베이스, 파일 또는 파일 그룹 백업으로 페이지 복원을 시작합니다. RESTORE DATABASE 문에서 PAGE 절을 사용하여 복원할 모든 페이지의 페이지 ID를 나열합니다.  
  
3.  가장 최근의 차등 백업을 적용합니다.  
  
4.  후속 로그 백업을 적용합니다.  
  
5.  복원된 페이지의 최종 LSN, 즉 마지막으로 복원된 페이지가 오프라인 상태로 된 시점을 포함하는 데이터베이스의 새 로그 백업을 만듭니다. 시퀀스에서 첫 번째 복원의 일부로 설정되는 최종 LSN은 다시 실행 대상 LSN입니다. 이 페이지를 포함하는 파일의 온라인 롤포워드는 다시 실행 대상 LSN에서 중지할 수 있습니다. 파일의 현재 다시 실행 대상 LSN을 알아보려면 **sys.master_files**의 **redo_target_lsn** 열을 확인합니다. 자세한 내용은 [sys.master_files&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)를 참조하세요.  
  
6.  새 로그 백업을 복원합니다. 새로운 이 로그 백업을 적용하면 페이지 복원이 완료되며 페이지를 사용할 수 있습니다.  
  
    > [!NOTE]  
    >  이 시퀀스는 파일 복원 시퀀스와 유사하며 동일한 시퀀스의 일부로 페이지 복원과 파일 복원을 모두 수행할 수도 있습니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 `B` 로 `NORECOVERY`파일의 손상된 4페이지를 복원합니다. 그런 다음 두 개의 로그 백업에 `NORECOVERY`를 적용하고 `RECOVERY`로 복원되는 비상 로그 백업을 실행합니다. 이 예에서는 온라인 복원을 수행합니다. 이 예에서 `B` 파일의 파일 ID는 `1`이고 손상된 페이지의 페이지 ID는 각각 `57`, `202`, `916`및 `1016`입니다.  
  
```sql  
RESTORE DATABASE <database> PAGE='1:57, 1:202, 1:916, 1:1016'  
   FROM <file_backup_of_file_B>   
   WITH NORECOVERY;  
RESTORE LOG <database> FROM <log_backup>   
   WITH NORECOVERY;  
RESTORE LOG <database> FROM <log_backup>   
   WITH NORECOVERY;   
BACKUP LOG <database> TO <new_log_backup>;   
RESTORE LOG <database> FROM <new_log_backup> WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [트랜잭션 로그 백업 적용&#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [suspect_pages 테이블 관리&#40;SQL Server&#41;](manage-the-suspect-pages-table-sql-server.md)   
 [SQL Server 데이터베이스 백업 및 복원](back-up-and-restore-of-sql-server-databases.md)  
  
  
