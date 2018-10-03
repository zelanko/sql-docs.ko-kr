---
title: 꽉 찬 트랜잭션 로그 문제 해결(SQL Server 오류 9002) | Microsoft 문서
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], full
- troubleshooting [SQL Server], full transaction log
- 9002 (Database Engine error)
- transaction logs [SQL Server], truncation
- backing up transaction logs [SQL Server], full logs
- transaction logs [SQL Server], full log
- full transaction logs [SQL Server]
ms.assetid: 0f23aa84-475d-40df-bed3-c923f8c1b520
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 75677d897c714828e23205490d68fd2e691b9b39
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48084913"
---
# <a name="troubleshoot-a-full-transaction-log-sql-server-error-9002"></a>꽉 찬 트랜잭션 로그 문제 해결(SQL Server 오류 9002)
  이 항목에서는 트랜잭션 로그가 꽉 찼을 때 알맞은 대처 방법에 대해 설명하고 앞으로 이런 상황을 방지하기 위한 방법을 제시합니다. 트랜잭션 로그가 꽉 차면 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 9002 오류가 발생합니다. 로그는 데이터베이스가 온라인 상태이거나 복구 중일 때 꽉 찰 수 있습니다. 데이터베이스가 온라인 상태일 때 로그가 꽉 차면 계속 온라인 상태로 유지되지만 데이터베이스를 읽을 수만 있고 업데이트할 수 없습니다. 복구 중에 로그가 꽉 차면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 데이터베이스를 RESOURCE PENDING으로 표시합니다. 두 경우 모두 사용자 동작을 통해 사용 가능한 로그 공간을 만들어야 합니다.  
  
## <a name="responding-to-a-full-transaction-log"></a>트랜잭션 로그가 꽉 찼을 경우 대처 방법  
 트랜잭션 로그가 꽉 찬 경우의 적절한 대처 방법은 로그가 꽉 차게 된 조건에 의해서도 영향을 받습니다. 지정된 경우에서 로그 잘림이 발생하지 않는 이유를 확인하려면 **sys.database** 카탈로그 뷰의 **log_reuse_wait** 및 **log_reuse_wait_desc** 열을 사용합니다. 자세한 내용은 [sys.databases&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)를 참조하세요. 로그 잘림을 지연시킬 수 있는 요소에 대한 자세한 내용은 [트랜잭션 로그&#40;SQL Server&#41;](the-transaction-log-sql-server.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  문제를 해결 한 후 9002 오류가 발생 했을 때 데이터베이스를 복구에서 하는 경우 ALTER DATABASE를 사용 하 여 데이터베이스를 복구할 *database_name* 를 온라인으로 설정 합니다.  
  
 트랜잭션 로그가 꽉 찬 경우의 대처 방법으로 다음 방법을 사용할 수도 있습니다.  
  
-   로그 백업  
  
-   로그가 자동으로 증가될 수 있도록 디스크 공간 확보  
  
-   공간이 충분한 디스크 드라이브로 로그 파일 이동  
  
-   로그 파일의 크기 증가  
  
-   다른 디스크에 로그 파일 추가  
  
-   장기 실행 트랜잭션 완료 또는 중지  
  
 이러한 방법에 대해서는 다음 섹션에서 설명합니다. 해당 상황에 가장 적합한 대처 방법을 선택하십시오.  
  
### <a name="backing-up-the-log"></a>로그 백업  
 전체 복구 모델 또는 대량 로그 복구 모델에서 트랜잭션 로그가 최근에 백업되지 않은 경우 백업하면 로그 잘림이 방지될 수 있습니다. 로그가 백업된 적이 없으면 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 로그를 마지막 백업 시점까지 자를 수 있도록 두 개의 로그 백업을 만들어야 합니다. 로그를 자르면 새 로그 레코드를 위한 공간이 늘어납니다. 로그가 다시 꽉 차지 않게 하려면 자주 로그 백업을 수행합니다.  
  
 **트랜잭션 로그 백업을 만들려면**  
  
> [!IMPORTANT]  
>  데이터베이스가 손상된 경우 [비상 로그 백업&#40;SQL Server&#41;](../backup-restore/tail-log-backups-sql-server.md)을 참조하세요.  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](../backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Backup.SqlBackup%2A> (SMO)  
  
### <a name="freeing-disk-space"></a>디스크 공간 늘리기  
 다른 파일을 삭제하거나 이동하여 데이터베이스의 트랜잭션 로그 파일이 들어 있는 디스크 드라이브의 디스크 공간을 늘릴 수 있습니다. 디스크 공간에 여유가 있으면 복구 시스템이 자동으로 로그 파일을 확장할 수 있습니다.  
  
### <a name="moving-the-log-file-to-a-different-disk"></a>로그 파일을 다른 디스크로 이동  
 현재 로그 파일이 들어 있는 드라이브에서 충분한 디스크 공간을 확보할 수 없으면 공간이 충분한 다른 드라이브로 파일을 이동하십시오.  
  
> [!IMPORTANT]  
>  로그 파일은 압축 파일 시스템에 저장할 수 없습니다.  
  
 **로그 파일을 이동 하려면**  
  
-   [데이터베이스 파일 이동](../databases/move-database-files.md)  
  
### <a name="increasing-the-size-of-a-log-file"></a>로그 파일의 크기 증가  
 로그 디스크에 사용 가능한 공간이 있으면 로그 파일의 크기를 늘릴 수 있습니다. 로그 파일의 최대 크기는 로그 파일당 2TB입니다.  
  
 **파일 크기를 늘리려면**  
  
 자동 증가를 사용하지 않으며 데이터베이스가 온라인 상태이고 디스크에서 충분한 공간을 사용할 수 있는 경우  
  
-   수동으로 파일 크기를 늘려 단일 증분을 생성합니다.  
  
-   ALTER DATABASE 문으로 FILEGROWTH 옵션에 대해 0이 아닌 증분을 설정하여 자동 증가를 설정합니다.  
  
> [!NOTE]  
>  두 경우 모두 현재 크기 제한에 도달하면 MAXSIZE 값을 늘리십시오.  
  
### <a name="adding-a-log-file-on-a-different-disk"></a>다른 디스크에 로그 파일 추가  
 ALTER DATABASE <database_name> ADD LOG FILE을 사용하여 공간이 충분한 다른 디스크의 데이터베이스에 새 로그 파일을 추가합니다.  
  
 **로그 파일을 추가 하려면**  
  
-   [데이터베이스에 데이터 또는 로그 파일 추가](../databases/add-data-or-log-files-to-a-database.md)  
  
## <a name="see-also"></a>관련 항목  
 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)   
 [트랜잭션 로그 파일의 크기 관리](manage-the-size-of-the-transaction-log-file.md)   
 [트랜잭션 로그 백업&#40;SQL Server&#41;](../backup-restore/transaction-log-backups-sql-server.md)   
 [sp_add_log_file_recover_suspect_db&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-add-log-file-recover-suspect-db-transact-sql)  
  
  
