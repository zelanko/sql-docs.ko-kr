---
title: 리소스 관리자를 사용하여 백업 압축을 통해 CPU 사용량 제한(Transact-SQL) | Microsoft 문서
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup compression [SQL Server], Resource Governor
- backup compression [SQL Server], CPU usage
- compression [SQL Server], backup compression
- backups [SQL Server], compression
- Resource Governor, backup compression
ms.assetid: 01796551-578d-4425-9b9e-d87210f7ba72
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d3094df3f5fff3a0dbeb70573236432202420224
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210542"
---
# <a name="use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql"></a>리소스 관리자를 사용하여 백업 압축을 통해 CPU 사용량 제한(Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  기본적으로 압축을 사용하여 백업하면 CPU 사용량이 크게 늘어나고 압축 프로세스로 사용되는 추가 CPU는 동시 작업에 악영향을 줄 수 있습니다. 따라서 CPU 경합이 발생하면 CPU 사용량이[Resource Governor](../../relational-databases/resource-governor/resource-governor.md) 로 제한되는 세션에서 우선 순위가 낮은 압축 백업을 만들 수 있습니다. 이 항목에서는 이와 같은 경우에 CPU 사용량을 제한하는 리소스 관리자 작업 그룹에 특정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자의 세션을 매핑하는 방법으로 이러한 세션을 분류하는 시나리오를 제공합니다.  
  
> [!IMPORTANT]  
>  주어진 리소스 관리자 시나리오에서 사용자 이름, 애플리케이션 이름을 비롯해 연결을 차별화하는 어떠한 요소라도 세션 분류의 기준이 될 수 있습니다. 자세한 내용은 [Resource Governor Classifier Function](../../relational-databases/resource-governor/resource-governor-classifier-function.md) 및 [Resource Governor Workload Group](../../relational-databases/resource-governor/resource-governor-workload-group.md)를 참조하세요.  
  
##  <a name="Top"></a> 이 항목에서는 다음과 같은 시나리오를 순서대로 다룹니다.  
  
1.  [우선 순위가 낮은 작업에 대한 로그인 및 사용자 설정](#setup_login_and_user)  
  
2.  [CPU 사용량을 제한하도록 리소스 관리자 구성](#configure_RG)  
  
3.  [현재 세션의 분류 확인(Transact-SQL)](#verifying)  
  
4.  [CPU가 제한된 세션을 사용하여 백업 압축](#creating_compressed_backup)  
  
##  <a name="setup_login_and_user"></a> 우선 순위가 낮은 작업에 대한 로그인 및 사용자 설정  
 이 항목의 시나리오에는 우선 순위가 낮은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 및 사용자가 필요합니다. 사용자 이름은 이 로그인에서 실행되는 세션을 분류하고 CPU 사용량을 제한하는 리소스 관리자 작업 그룹으로 이러한 세션을 라우팅하는 데 사용됩니다.  
  
 다음 절차에서는 이러한 목적에 맞게 로그인 및 사용자를 설정하는 단계를 설명하며, 그 다음에는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 예로 "예 1: 로그인 및 사용자 설정(Transact-SQL)"이 제공됩니다.  
  
### <a name="to-set-up-a-login-and-database-user-for-classifying-sessions"></a>세션 분류를 위한 로그인 및 데이터베이스 사용자를 설정하려면  
  
1.  우선 순위가 낮은 압축된 백업을 만들기 위한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 만듭니다.  
  
     **로그인을 만들려면**  
  
    -   [로그인 만들기](../../relational-databases/security/authentication-access/create-a-login.md)  
  
    -   [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)  
  
2.  필요에 따라 이 로그인에 VIEW SERVER STATE를 부여합니다.  
  
    -   [GRANT 시스템 개체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-system-object-permissions-transact-sql.md)  
  
     자세한 내용은 [GRANT 데이터베이스 보안 주체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)을 참조하세요.  
  
3.  이 로그인의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자를 만듭니다.  
  
     **사용자를 만들려면**  
  
    -   [데이터베이스 사용자 만들기](../../relational-databases/security/authentication-access/create-a-database-user.md)  
  
    -   [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)  
  
4.  이 로그인 및 사용자의 세션에서 지정된 데이터베이스를 백업하도록 하려면 해당 데이터베이스의 db_backupoperator 데이터베이스 역할에 사용자를 추가합니다. 이 사용자가 백업할 각 데이터베이스에 대해 이를 수행합니다. 필요에 따라 다른 고정 데이터베이스 역할에 사용자를 추가합니다.  
  
     **고정 데이터베이스 역할에 사용자를 추가하려면**  
  
    -   [sp_addrolemember&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)  
  
     자세한 내용은 [GRANT 데이터베이스 보안 주체 사용 권한&#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-principal-permissions-transact-sql.md)을 참조하세요.  
  
### <a name="example-a-setting-up-a-login-and-user-transact-sql"></a>예 1: 로그인 및 사용자 설정(Transact-SQL)  
 다음 예는 우선 순위가 낮은 백업을 위한 새 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 및 사용자를 만들도록 선택한 경우에만 해당합니다. 또는 적절한 기존의 로그인 및 사용자가 있는 경우 이를 사용할 수 있습니다.  
  
> [!IMPORTANT]  
>  다음 예제에서는 샘플 로그인 및 사용자 이름 *domain_name*`\MAX_CPU`을 사용합니다. 이를 우선 순위가 낮은 압축된 백업을 만들 때 사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 및 사용자로 대체합니다.  
  
 이 예제에서는 *domain_name*`\MAX_CPU` Windows 계정의 로그인을 만든 다음 이 로그인에 VIEW SERVER STATE 권한을 부여합니다. 이 권한을 통해 로그인 세션의 리소스 관리자 분류를 확인할 수 있습니다. 그런 다음 *domain_name*`\MAX_CPU` 의 사용자를 만들어 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 샘플 데이터베이스에 대한 db_backupoperator 고정 데이터베이스 역할에 추가합니다. 이 사용자 이름은 리소스 관리자 분류자 함수에 의해 사용됩니다.  
  
```sql  
-- Create a SQL Server login for low-priority operations  
USE master;  
CREATE LOGIN [domain_name\MAX_CPU] FROM WINDOWS;  
GRANT VIEW SERVER STATE TO [domain_name\MAX_CPU];  
GO  
-- Create a SQL Server user in AdventureWorks2012 for this login  
USE AdventureWorks2012;  
CREATE USER [domain_name\MAX_CPU] FOR LOGIN [domain_name\MAX_CPU];  
EXEC sp_addrolemember 'db_backupoperator', 'domain_name\MAX_CPU';  
GO  
  
```  
  
 [&#91;맨 위로 이동&#93;](#Top)  
  
##  <a name="configure_RG"></a> CPU 사용량을 제한하도록 리소스 관리자 구성  
  
> [!NOTE]  
>  리소스 관리자가 설정되어 있는지 확인합니다. 자세한 내용은 [Resource Governor 사용](../../relational-databases/resource-governor/enable-resource-governor.md)을 참조하세요.  
  
 이 리소스 관리자 시나리오는 다음과 같은 기본 단계로 구성됩니다.  
  
1.  CPU 충돌이 발생하면 리소스 풀의 요청에 지정되는 최대 평균 CPU 대역폭을 제한하는 리소스 관리자 리소스 풀을 만들고 구성합니다.  
  
2.  이 풀을 사용하는 리소스 관리자 작업 그룹을 만들고 구성합니다.  
  
3.  *분류자 함수*를 만듭니다. 분류자 함수는 UDF(사용자 정의 함수)로, Resource Governor는 세션을 적절한 작업 그룹으로 라우팅되도록 분류하기 위해 이 함수의 반환 값을 사용합니다.  
  
4.  분류자 함수를 리소스 관리자에 등록합니다.  
  
5.  변경 내용을 리소스 관리자 메모리 내 구성에 적용합니다.  
  
> [!NOTE]  
>  Resource Governor 리소스 풀, 작업 그룹 및 분류에 대한 자세한 내용은 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)를 참조하세요.  
  
 이러한 단계를 위한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 "CPU 사용량을 제한하도록 리소스 관리자를 구성하려면" 절차에 설명되어 있습니다. 그 다음에는 이 절차의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 예가 나옵니다.  
  
 **리소스 관리자를 구성하려면(SQL Server Management Studio)**  
  
-   [템플릿을 사용하여 리소스 관리자 구성](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)  
  
-   [리소스 풀 만들기](../../relational-databases/resource-governor/create-a-resource-pool.md)  
  
-   [작업 그룹 만들기](../../relational-databases/resource-governor/create-a-workload-group.md)  
  
### <a name="to-configure-resource-governor-for-limiting-cpu-usage-transact-sql"></a>CPU 사용량을 제한하도록 리소스 관리자를 구성하려면(Transact-SQL)  
  
1.  [CREATE RESOURCE POOL](../../t-sql/statements/create-resource-pool-transact-sql.md) 문을 실행하여 리소스 풀을 만듭니다. 이 절차에 대한 예에서는 다음 구문을 사용합니다.  
  
     *CREATE RESOURCE POOL pool_name* WITH ( MAX_CPU_PERCENT = *value* );  
  
     *Value* 는 최대 평균 CPU 대역폭의 비율을 나타내는 1에서 100까지의 정수입니다. 적절한 값은 해당 환경에 따라 달라집니다. 이 항목의 예에서는 설명을 위해 20% 비율을 사용합니다(MAX_CPU_PERCENT = 20).  
  
2.  [CREATE WORKLOAD GROUP](../../t-sql/statements/create-workload-group-transact-sql.md) 문을 실행하여 CPU 사용량을 관리하려는 우선 순위가 낮은 작업에 대한 작업 그룹을 만듭니다. 이 절차에 대한 예에서는 다음 구문을 사용합니다.  
  
     CREATE WORKLOAD GROUP *group_name* USING *pool_name*;  
  
3.  [CREATE FUNCTION](../../t-sql/statements/create-function-transact-sql.md) 문을 실행하여 이전 단계에서 만든 작업 그룹을 우선 순위가 낮은 로그인의 사용자에 매핑하는 분류자 함수를 만듭니다. 이 절차에 대한 예에서는 다음 구문을 사용합니다.  
  
     CREATE FUNCTION [*schema_name*.]*function_name*() RETURNS sysname  
  
     WITH SCHEMABINDING  
  
     AS  
  
     BEGIN  
  
     DECLARE @workload_group_name AS *sysname*  
  
     IF (SUSER_NAME() = '*user_of_low_priority_login*')  
  
     SET @workload_group_name = '*workload_group_name*'  
  
     RETURN @workload_group_name  
  
     END  
  
     이 CREATE FUNCTION 문의 구성 요소에 대한 자세한 내용은 다음을 참조하십시오.  
  
    -   [DECLARE @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
  
    -   [SUSER_SNAME&#40;Transact-SQL&#41;](../../t-sql/functions/suser-sname-transact-sql.md)  
  
        > [!IMPORTANT]  
        >  SUSER_NAME은 분류자 함수에 사용할 수 있는 여러 시스템 함수 중 하나일 뿐입니다. 자세한 내용은 [분류자 사용자 정의 함수 만들기 및 테스트](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)를 참조하세요.  
  
    -   [SET @local_variable&#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md).  
  
4.  [ALTER RESOURCE GOVERNOR](../../t-sql/statements/alter-resource-governor-transact-sql.md) 문을 실행하여 리소스 관리자에 분류자 함수를 등록합니다. 이 절차에 대한 예에서는 다음 구문을 사용합니다.  
  
     ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION = *schema_name*.*function_name*);  
  
5.  두 번째 ALTER RESOURCE GOVERNOR 문을 실행하여 다음과 같이 변경 내용을 리소스 관리자 메모리 내 구성에 적용합니다.  
  
    ```  
    ALTER RESOURCE GOVERNOR RECONFIGURE;  
    ```  
  
### <a name="example-b-configuring-resource-governor-transact-sql"></a>예 2: 리소스 관리자 구성(Transact-SQL)  
 다음 예에서는 하나의 트랜잭션 내에서 다음과 같은 단계를 수행합니다.  
  
1.  `pMAX_CPU_PERCENT_20` 리소스 풀을 만듭니다.  
  
2.  `gMAX_CPU_PERCENT_20` 작업 그룹을 만듭니다.  
  
3.  이전 예에서 만든 사용자 이름을 사용하는 `rgclassifier_MAX_CPU()` 분류자 함수를 만듭니다.  
  
4.  분류자 함수를 리소스 관리자에 등록합니다.  
  
 트랜잭션을 커밋한 후 예에서는 ALTER WORKLOAD GROUP 또는 ALTER RESOURCE POOL 문에 요청된 구성 변경 내용을 적용합니다.  
  
> [!IMPORTANT]  
>  다음 예에서는 “예 1: 로그인 및 사용자 설정(Transact-SQL)"에서 만든 예제 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자의 사용자 이름인 *domain_name*`\MAX_CPU`을 사용합니다. 이 이름을 우선 순위가 낮은 압축된 백업을 만드는 데 사용할 로그인 사용자의 이름으로 대체합니다.  
  
```sql  
-- Configure Resource Governor.  
BEGIN TRAN  
USE master;  
-- Create a resource pool that sets the MAX_CPU_PERCENT to 20%.   
CREATE RESOURCE POOL pMAX_CPU_PERCENT_20  
   WITH  
      (MAX_CPU_PERCENT = 20);  
GO  
-- Create a workload group to use this pool.   
CREATE WORKLOAD GROUP gMAX_CPU_PERCENT_20  
USING pMAX_CPU_PERCENT_20;  
GO  
-- Create a classification function.  
-- Note that any request that does not get classified goes into   
-- the 'Default' group.  
CREATE FUNCTION dbo.rgclassifier_MAX_CPU() RETURNS sysname   
WITH SCHEMABINDING  
AS  
BEGIN  
    DECLARE @workload_group_name AS sysname  
      IF (SUSER_NAME() = 'domain_name\MAX_CPU')  
          SET @workload_group_name = 'gMAX_CPU_PERCENT_20'  
    RETURN @workload_group_name  
END;  
GO  
  
-- Register the classifier function with Resource Governor.  
ALTER RESOURCE GOVERNOR WITH (CLASSIFIER_FUNCTION= dbo.rgclassifier_MAX_CPU);  
COMMIT TRAN;  
GO  
-- Start Resource Governor  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
  
```  
  
 [&#91;맨 위로 이동&#93;](#Top)  
  
##  <a name="verifying"></a> 현재 세션의 분류 확인(Transact-SQL)  
 필요에 따라 분류자 함수에 지정한 사용자로 로그인한 후 개체 탐색기에서 다음 [SELECT](../../t-sql/queries/select-transact-sql.md) 문을 실행하여 세션 분류를 확인합니다.  
  
```sql  
USE master;  
SELECT sess.session_id, sess.login_name, sess.group_id, grps.name   
FROM sys.dm_exec_sessions AS sess   
JOIN sys.dm_resource_governor_workload_groups AS grps   
    ON sess.group_id = grps.group_id  
WHERE session_id > 50;  
GO  
```  
  
 결과 창의 **name** 열에는 분류자 함수에서 지정한 작업 그룹 이름에 대한 하나 이상의 세션이 나열됩니다.  
  
> [!NOTE]  
>  이 SELECT 문에서 호출하는 동적 관리 뷰에 대한 자세한 내용은 [sys.dm_exec_sessions&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md) 및 [sys.dm_resource_governor_workload_groups&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-workload-groups-transact-sql.md)를 참조하세요.  
  
 [&#91;맨 위로 이동&#93;](#Top)  
  
##  <a name="creating_compressed_backup"></a> CPU가 제한된 세션을 사용하여 백업 압축  
 최대 CPU가 제한된 세션에서 압축된 백업을 만들려면 분류자 함수에 지정된 사용자로 로그인합니다. 백업 명령에 WITH COMPRESSION([!INCLUDE[tsql](../../includes/tsql-md.md)])을 지정하거나 **백업 압축**([!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)])을 선택합니다. 압축된 데이터베이스 백업을 만들려면 [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)를 참조하세요.  
  
### <a name="example-c-creating-a-compressed-backup-transact-sql"></a>예 3: 압축된 백업 만들기(Transact-SQL)  
 다음 [BACKUP](../../t-sql/statements/backup-transact-sql.md) 예에서는 새로 형식이 지정된 백업 파일인 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 에 `Z:\SQLServerBackups\AdvWorksData.bak`데이터베이스의 압축된 전체 백업을 만듭니다.  
  
```sql  
--Run backup statement in the gBackup session.  
BACKUP DATABASE AdventureWorks2012 TO DISK='Z:\SQLServerBackups\AdvWorksData.bak'   
WITH   
   FORMAT,   
   MEDIADESCRIPTION='AdventureWorks2012 Compressed Data Backups'  
   DESCRIPTION='First database backup on AdventureWorks2012 Compressed Data Backups media set'  
   COMPRESSION;  
GO  
```  
  
 [&#91;맨 위로 이동&#93;](#Top)  
  
## <a name="see-also"></a>참고 항목  
 [분류자 사용자 정의 함수 만들기 및 테스트](../../relational-databases/resource-governor/create-and-test-a-classifier-user-defined-function.md)   
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)  
  
  
