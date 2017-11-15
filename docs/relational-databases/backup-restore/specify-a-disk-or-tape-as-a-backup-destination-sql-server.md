---
title: "디스크 또는 테이프를 백업 대상으로 지정(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backup devices [SQL Server], tapes
- backing up databases [SQL Server], tapes
- database backups [SQL Server], tapes
- backup devices [SQL Server], disks
- disk backup devices [SQL Server]
- database backups [SQL Server], disks
- backing up databases [SQL Server], disks
- backups [SQL Server], creating
- tape backup devices, backing up
ms.assetid: e391f452-ed8c-4b40-b846-ac3881271b94
caps.latest.revision: "30"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 43c089f2b9e3dbca470a44c56c4b51ad2d38aa44
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="specify-a-disk-or-tape-as-a-backup-destination-sql-server"></a>디스크 또는 테이프를 백업 대상으로 지정(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 백업 대상으로 디스크 또는 테이프를 지정하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  테이프 백업 장치에 대한 지원은 나중 버전의 SQL Server에서 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 디스크나 테이프를 백업 대상으로 지정합니다.**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 사용 권한  
 BACKUP DATABASE 및 BACKUP LOG 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_owner** 및 **db_backupoperator** 고정 데이터베이스 역할의 멤버로 설정됩니다.  
  
 백업 장치의 물리적 파일에서 발생하는 소유권과 사용 권한 문제는 백업 작업에 영향을 미칠 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 장치를 읽고 쓸 수 있어야 하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행되는 계정에는 쓰기 권한이 있어야 합니다. 그러나 시스템 테이블의 백업 장치에 대한 항목을 추가하는 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)는 파일 액세스 권한을 확인하지 않습니다. 백업 장치의 물리적 파일에서 발생하는 이러한 문제는 백업 또는 복원을 시도할 때 실제 리소스를 액세스하기 전까지는 발생하지 않습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-specify-a-disk-or-tape-as-a-backup-destination"></a>디스크나 테이프를 백업 대상으로 지정하려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스** 를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **백업**을 클릭합니다. **데이터베이스 백업** 대화 상자가 나타납니다.  
  
4.  **일반** 페이지의 **대상** 섹션에서 **디스크** 또는 **테이프**를 선택합니다. **추가**를 클릭하면 단일 미디어 세트를 포함하는 디스크나 테이프 드라이브에 대한 경로를 64개까지 선택할 수 있습니다.  
  
     백업 대상을 제거하려면 해당 대상을 선택한 다음 **제거**를 클릭합니다. 백업 대상의 내용을 보려면 선택한 다음 **내용**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-specify-a-disk-or-tape-as-a-backup-destination"></a>디스크나 테이프를 백업 대상으로 지정하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  [BACKUP](../../t-sql/statements/backup-transact-sql.md) 문에서 파일 또는 장치와 해당 물리적 이름을 지정합니다. 이 예에서는 `AdventureWorks2012` 데이터베이스를 디스크 파일 `Z:\SQLServerBackups\AdventureWorks2012.Bak`에 백업합니다.  
  
```  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)   
 [파일 및 파일 그룹 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)   
 [디스크 파일에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)   
 [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)   
 [테이프 드라이브에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
  
