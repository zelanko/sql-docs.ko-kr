---
title: 기존에서 파일 및 파일 그룹 복원
description: 이 문서에서는 SQL Server에서 SQL Server Management Studio 또는 Transact-SQL을 사용하여 기존 파일에서 파일 및 파일 그룹을 복원하는 방법을 보여 줍니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring files [SQL Server], how-to topics
- restoring files [SQL Server], steps
- file restores [SQL Server], how-to topics
- filegroups [SQL Server], restoring
- restoring filegroups [SQL Server]
- overwriting filegroups
- overwriting files
ms.assetid: 517e07eb-9685-4b06-90af-b1cc496700b7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: b5d477202b26c06ed2507ebd87dc908ad4a845c7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "82180744"
---
# <a name="restore-files-and-filegroups-over-existing-files-sql-server"></a>기존 파일에서 파일 및 파일 그룹 복원(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 기존 파일에 대해 파일 및 파일 그룹을 복원하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 기존 파일에서 파일과 파일 그룹을 복원합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> 제한 사항  
  
-   파일과 파일 그룹을 복원하는 시스템 관리자가 현재 복원될 데이터베이스를 사용하고 있는 유일한 사용자여야 합니다.  
  
-   RESTORE는 명시적 또는 암시적 트랜잭션에서 사용할 수 없습니다.  
  
-   전체 복구 모델 또는 대량 로그 복구 모델의 경우 파일을 복원하려면 먼저 활성 트랜잭션 로그(비상 로그라고도 함)를 백업해야 합니다. 자세한 내용은 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)데이터베이스를 새 위치로 복원하고 선택적으로 데이터베이스 이름을 바꾸는 방법을 설명합니다.  
  
-   암호화된 데이터베이스를 복원하려면 데이터베이스를 암호화하는 데 사용된 인증서 또는 비대칭 키에 대한 액세스 권한이 있어야 합니다. 인증서 또는 비대칭 키가 없으면 데이터베이스를 복원할 수 없습니다. 따라서 데이터베이스 암호화 키를 암호화하는 데 사용되는 인증서는 백업이 필요한 동안에는 유지되어야 합니다. 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)을 참조하세요.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 복원할 데이터베이스가 없으면 CREATE DATABASE 권한이 있어야 RESTORE를 실행할 수 있습니다. 데이터베이스가 있으면 RESTORE 권한은 기본적으로 **sysadmin** 및 **dbcreator** 고정 서버 역할의 멤버와 데이터베이스의 소유자(**dbo**)에 설정됩니다. FROM DATABASE_SNAPSHOT 옵션의 경우 데이터베이스가 항상 있습니다.  
  
 멤버 자격 정보를 서버에서 항상 사용할 수 있는 역할에 RESTORE 권한이 제공됩니다. 고정 데이터베이스 역할의 멤버 자격은 데이터베이스가 액세스 가능한 상태이며 손상되지 않은 경우에만 확인할 수 있는데, RESTORE 실행 시 데이터베이스가 항상 이러한 상태인 것은 아니므로 **db_owner** 고정 데이터베이스 역할의 멤버에게는 RESTORE 권한이 없습니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-restore-files-and-filegroups-over-existing-files"></a>기존 파일에서 파일과 파일 그룹을 복원하려면  
  
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 인스턴스에 연결하고 해당 인스턴스를 확장한 다음 **데이터베이스**를 확장합니다.  
  
2.  원하는 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**, **복원**을 차례로 가리킨 다음 **파일 및 파일 그룹**을 클릭합니다.  
  
3.  **일반** 페이지의 **데이터베이스** 목록 상자에 복원할 데이터베이스를 입력합니다. 새 데이터베이스를 입력하거나 드롭다운 목록에서 기존 데이터베이스를 선택할 수 있습니다. 이 목록에는 시스템 데이터베이스인 **master** 및 **tempdb**를 제외한 서버의 모든 데이터베이스가 포함되어 있습니다.  
  
4.  복원할 백업 세트의 원본 및 위치를 지정하려면 다음 옵션 중 하나를 클릭합니다.  
  
    -   **데이터베이스**  
  
         목록 상자에 데이터베이스 이름을 입력합니다. 이 목록에는 **msdb** 백업 기록에 따라 백업된 데이터베이스만 포함되어 있습니다.  
  
    -   **디바이스**  
  
         찾아보기 단추를 클릭합니다. **백업 디바이스 지정** 대화 상자에서 **백업 미디어 유형** 목록 상자에 나열된 디바이스 유형 중 하나를 선택합니다. **백업 미디어** 목록 상자에서 하나 이상의 디바이스를 선택하려면 **추가**를 클릭합니다.  
  
         원하는 디바이스를 **백업 미디어** 목록 상자에 추가한 후 **확인** 을 클릭하여 **일반** 페이지로 돌아갑니다.  
  
5.  **복원에 사용할 백업 세트 선택** 표에서 복원할 백업을 선택합니다. 이 표는 지정한 위치에서 사용 가능한 백업을 표시합니다. 기본적으로 복구 계획이 제안됩니다. 제안된 복구 계획을 재정의하려면 표에서 선택 항목을 변경합니다. 선택 취소된 백업에 의존하는 모든 백업은 자동으로 선택 취소됩니다.  
  
    |열 머리글|값|  
    |-----------------|------------|  
    |**복원**|확인란이 선택되어 있으면 백업 세트가 복원됩니다.|  
    |**이름**|백업 세트의 이름입니다.|  
    |**파일 유형**|백업의 데이터 형식인 **데이터**, **로그** 또는 **Filestream 데이터**를 지정합니다. 테이블에 포함된 데이터는 **데이터** 파일에 있고, 트랜잭션 로그 데이터는 **로그** 파일에 있으며, 파일 시스템에 저장되는 BLOB(Binary Large Object) 데이터는 **Filestream 데이터** 파일에 있습니다.|  
    |**형식**|수행된 백업 유형: **전체**, **차등** 또는 **트랜잭션 로그**가 될 수 있습니다.|  
    |**Server**|백업 작업을 수행한 데이터베이스 엔진 인스턴스의 이름입니다.|  
    |**논리적 파일 이름**|파일의 논리적 이름입니다.|  
    |**Database**|백업 작업과 관련된 데이터베이스의 이름입니다.|  
    |**Start Date**|클라이언트의 국가별 설정으로 표시되는 백업 작업 시작 날짜 및 시간입니다.|  
    |**완료 날짜**|클라이언트의 국가별 설정으로 표시되는 백업 작업 완료 날짜 및 시간입니다.|  
    |**크기**|백업 세트의 크기를 바이트 단위로 표시한 것입니다.|  
    |**사용자 이름**|백업 작업을 수행한 사용자의 이름입니다.|  
  
6.  **페이지 선택** 창에서 **옵션** 페이지를 클릭합니다.  
  
7.  **복원 옵션** 패널에서 **기존 데이터베이스 덮어쓰기(WITH REPLACE)** 를 선택합니다. 복원 작업은 이름이 동일한 데이터베이스 또는 파일이 이미 있더라도 기존 데이터베이스 및 관련 파일을 덮어씁니다.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-restore-files-and-filegroups-over-existing-files"></a>기존 파일에서 파일과 파일 그룹을 복원하려면  
  
1.  RESTORE DATABASE 문을 실행하여 파일과 파일 그룹 백업을 복원합니다. 이때 다음을 지정합니다.  
  
    -   복원할 데이터베이스의 이름  
  
    -   복원할 전체 데이터베이스 백업이 있는 백업 디바이스  
  
    -   복원할 각 파일에 대한 FILE 절  
  
    -   복원할 각 파일 그룹에 대한 FILEGROUP 절  
  
    -   각 파일이 같은 이름과 위치에 있는 기존 파일로 복원될 수 있도록 지정하기 위한 REPLACE 옵션  
  
        > [!CAUTION]  
        >  REPLACE 옵션을 사용할 때는 주의하세요. 자세한 내용은 을(를) 참조하세요.  
  
    -   NORECOVERY 옵션. 백업을 만든 후 해당 파일들을 수정하지 않았으면 RECOVERY 절을 지정합니다.  
  
2.  파일 백업을 만든 후에 파일이 수정된 경우에는 RESTORE LOG 문을 실행하여 트랜잭션 로그 백업을 적용합니다. 이때 다음을 지정합니다.  
  
    -   트랜잭션 로그가 적용될 데이터베이스의 이름  
  
    -   트랜잭션 로그 백업이 복원될 원본 백업 디바이스  
  
    -   현재 트랜잭션 로그 백업 다음에 적용할 다른 트랜잭션 로그 백업이 있으면 NORECOVERY 절을 지정하고 없으면 RECOVERY 절을 지정합니다.  
  
         트랜잭션 로그 백업이 적용되는 경우 파일과 파일 그룹을 백업한 시점이 포함되어야 합니다.  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 `MyNwind` 데이터베이스의 파일과 파일 그룹을 복원하고 같은 이름의 기존 파일을 모두 바꿉니다. 또한 현재 시간으로 데이터베이스를 복원하기 위한 두 개의 트랜잭션 로그가 적용됩니다.  
  
```sql  
USE master;  
GO  
-- Restore the files and filesgroups for MyNwind.  
RESTORE DATABASE MyNwind  
   FILE = 'MyNwind_data_1',  
   FILEGROUP = 'new_customers',  
   FILE = 'MyNwind_data_2',  
   FILEGROUP = 'first_qtr_sales'  
   FROM MyNwind_1  
   WITH NORECOVERY,  
   REPLACE;  
GO  
-- Apply the first transaction log backup.  
RESTORE LOG MyNwind  
   FROM MyNwind_log1  
   WITH NORECOVERY;  
GO  
-- Apply the last transaction log backup.  
RESTORE LOG MyNwind  
   FROM MyNwind_log2  
   WITH RECOVERY;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)   
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [파일 및 파일 그룹 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)   
 [백업 및 복원으로 데이터베이스 복사](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)  
  
  
