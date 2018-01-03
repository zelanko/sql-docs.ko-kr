---
title: "백업의 만료 날짜 설정(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backing up databases [SQL Server], expiration dates
- expiration [SQL Server]
- database backups [SQL Server], expiration dates
ms.assetid: 76e814df-6487-4893-9f09-7759f1863a5c
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2ce756c5d3083c2bf072f4fa894d8b9a23143a27
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/02/2018
---
# <a name="set-the-expiration-date-on-a-backup-sql-server"></a>백업의 만료 날짜 설정(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 백업에 대한 만료 날짜를 설정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 백업의 만료 날짜를 설정합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 BACKUP DATABASE 및 BACKUP LOG 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_owner** 및 **db_backupoperator** 고정 데이터베이스 역할의 멤버로 설정됩니다.  
  
 백업 장치의 물리적 파일에서 발생하는 소유권과 사용 권한 문제는 백업 작업에 영향을 미칠 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 장치를 읽고 쓸 수 있어야 하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행되는 계정에는 쓰기 권한이 있어야 합니다. 그러나 시스템 테이블의 백업 장치에 대한 항목을 추가하는 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)는 파일 액세스 권한을 확인하지 않습니다. 백업 장치의 물리적 파일에서 발생하는 이러한 문제는 백업 또는 복원을 시도할 때 실제 리소스를 액세스하기 전까지는 발생하지 않습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-set-the-expiration-date-on-a-backup"></a>백업의 만료 날짜를 설정하려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스** 를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **백업**을 클릭합니다. **데이터베이스 백업** 대화 상자가 나타납니다.  
  
4.  **일반** 페이지에서 백업 세트를 다른 백업으로 덮어쓸 수 있는 만료 날짜를 **백업 세트 만료 기한**에 지정합니다.  
  
    -   백업 세트가 특정 일수가 지난 후에 만료되도록 하려면 **다음 이후** (기본 옵션)를 클릭한 다음 백업 세트를 만든 후 백업 세트가 만료되기까지 경과해야 하는 일수를 입력합니다. 이 값은 0일에서 99999일 사이일 수 있습니다. 값 0일은 백업 세트 기간 제한이 없음을 의미합니다.  
  
         기본값은 **서버 속성** 대화 상자( **데이터베이스 설정** 페이지)의**백업 미디어 기본 보존 기간(일)** 옵션에 설정되어 있습니다. 이 페이지에 액세스하려면 개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 속성을 선택한 다음 **데이터베이스 설정** 페이지를 선택합니다.  
  
    -   백업 세트가 특정 일자에 만료되게 하려면 **날짜**를 클릭한 다음 백업 세트가 만료될 날짜를 입력합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-set-the-expiration-date-on-a-backup"></a>백업의 만료 날짜를 설정하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  [BACKUP](../../t-sql/statements/backup-transact-sql.md) 문에서 EXPIREDATE 또는 RETAINDAYS 옵션을 지정하여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 이 백업을 덮어 쓸 수 있는 시간을 확인합니다. 두 옵션 모두 지정하지 않으면 [미디어 보존](../../database-engine/configure-windows/configure-the-media-retention-server-configuration-option.md) 서버 구성 설정에 따라 만료 날짜가 결정됩니다. 이 예에서는 `EXPIREDATE` 옵션을 사용하여 만료 날짜를 2015년 6월 30일(`6/30/2015`)로 지정합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
 TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
   WITH EXPIREDATE = '6/30/2015' ;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)   
 [파일 및 파일 그룹 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
  
