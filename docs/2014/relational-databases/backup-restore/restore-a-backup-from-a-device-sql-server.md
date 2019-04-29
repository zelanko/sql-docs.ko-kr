---
title: 디바이스에서 백업 복원(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring databases [SQL Server], device restores
- backup devices [SQL Server], restoring from
- database restores [SQL Server], device restores
- devices [SQL Server]
ms.assetid: 6e139de7-7de2-4d18-9df0-beac31ba7ff1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f5e272dde5ca7a3c0ff7246d42131f1e70331689
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62921959"
---
# <a name="restore-a-backup-from-a-device-sql-server"></a>디바이스에서 백업 복원(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 디바이스에서 백업을 복원하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  Windows Azure Blob 저장소 서비스로 SQL Server 백업하는 방법에 대한 자세한 내용은 [Windows Azure Blob 저장소 서비스로 SQL Server 백업 및 복원](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하십시오.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [보안](#Security)  
  
-   **다음을 사용하여 장치에서 백업을 복원합니다.**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 복원할 데이터베이스가 없으면 CREATE DATABASE 권한이 있어야 RESTORE를 실행할 수 있습니다. 데이터베이스가 있으면 RESTORE 권한은 기본적으로 **sysadmin** 및 **dbcreator** 고정 서버 역할의 멤버와 데이터베이스의 소유자(**dbo**)에 설정됩니다. FROM DATABASE_SNAPSHOT 옵션의 경우 데이터베이스가 항상 있습니다.  
  
 멤버 자격 정보를 서버에서 항상 사용할 수 있는 역할에 RESTORE 권한이 제공됩니다. 고정 데이터베이스 역할의 멤버 자격은 데이터베이스가 액세스 가능한 상태이며 손상되지 않은 경우에만 확인할 수 있는데, RESTORE 실행 시 데이터베이스가 항상 이러한 상태인 것은 아니므로 **db_owner** 고정 데이터베이스 역할의 멤버에게는 RESTORE 권한이 없습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-restore-a-backup-from-a-device"></a>디바이스에서 백업을 복원하려면  
  
1.   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스** 를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **복원**을 클릭합니다.  
  
4.  원하는 복원 작업의 유형(**데이터베이스**, **파일 및 파일 그룹**또는 **트랜잭션 로그**)을 클릭합니다. 이렇게 하면 해당되는 복원 대화 상자가 열립니다.  
  
5.  **일반** 페이지의 **복원 원본** 섹션에서 **장치**를 클릭합니다.  
  
6.  **장치** 입력란에 대한 찾아보기 단추를 클릭합니다. **백업 지정** 대화 상자가 열립니다.  
  
7.  **백업 미디어** 입력란에서 **백업 장치**를 선택하고 **추가** 단추를 클릭하여 **백업 장치 선택** 대화 상자를 엽니다.  
  
8.  **백업 장치** 입력란에서 복원 작업에 사용하려는 장치를 선택합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-restore-a-backup-from-a-device"></a>디바이스에서 백업을 복원하려면  
  
1.  [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결합니다.  
  
2.  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql) 문에서 백업 작업에 사용할 논리적 백업 장치나 물리적 백업 장치를 지정합니다. 이 예에서는 실제 이름이 `Z:\SQLServerBackups\AdventureWorks2012.bak`인 디스크 파일로부터 복원을 수행합니다.  
  
```sql  
RESTORE DATABASE AdventureWorks2012  
   FROM DISK = 'Z:\SQLServerBackups\AdventureWorks2012.bak' ;  
  
```  
  
## <a name="see-also"></a>관련 항목  
 [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)   
 [RESTORE HEADERONLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-headeronly-transact-sql)   
 [RESTORE LABELONLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-labelonly-transact-sql)   
 [RESTORE VERIFYONLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-verifyonly-transact-sql)   
 [단순 복구 모델에서 데이터베이스 백업 복원&#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)   
 [데이터베이스 백업 복원 &#40;SQL Server Management Studio&#41;](restore-a-database-backup-using-ssms.md)   
 [차등 데이터베이스 백업 복원&#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)   
 [데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)   
 [파일 및 파일 그룹 백업&#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)   
 [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)   
 [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
  
