---
title: 복사 전용 백업(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- copy-only backups [SQL Server]
- COPY_ONLY option [BACKUP statement]
- backups [SQL Server], copy-only backups
ms.assetid: f82d6918-a5a7-4af8-868e-4247f5b00c52
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 96267b98d7e17b920e0a7cee70b69e4c964584e4
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798010"
---
# <a name="copy-only-backups-sql-server"></a>복사 전용 백업(SQL Server)
  *복사 전용 백업* 은 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 시퀀스와 독립적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업입니다. 일반적으로 백업을 수행하면 데이터베이스가 변경되므로 이후 백업이 복원되는 방식에 영향을 주게 됩니다. 그러나 백업 전체에 영향을 주지 않고 특별한 용도로 백업을 수행한 다음 데이터베이스에 대한 프로시저를 복원하는 것이 유용할 수도 있습니다. 이러한 용도로 복사 전용 백업이 제공됩니다.  
  
 복사 전용 백업의 종류는 다음과 같습니다.  
  
-   복사 전용 전체 백업(모든 복구 모델)  
  
     복사 전용 백업은 차등 기반 또는 차등 백업으로 사용될 수 없으며 차등 기반에 영향을 미치지 않습니다.  
  
     복사 전용 전체 백업을 복원하는 과정은 다른 전체 백업을 복원하는 과정과 동일합니다.  
  
-   복사 전용 로그 백업(전체 복구 모델 및 대량 로그 복구 모델 전용)  
  
     복사 전용 로그 백업은 기존 로그 보관 지점을 유지하므로 정기적인 로그 백업 시퀀스에 영향을 주지 않습니다. 복사 전용 로그 백업은 일반적으로 불필요한 백업입니다. 대신 WITH NORECOVERY를 사용하여 새 정기 로그 백업을 만든 다음 해당 백업을 복원 시퀀스에 필요한 모든 이전 로그 백업과 함께 사용할 수 있습니다. 하지만 복사 전용 로그 백업은 온라인 복원에도 유용할 수 있습니다. 해당 예제를 보려면 [예제: 읽기-쓰기 파일의 온라인 복원&#40;전체 복구 모델&#41;](example-online-restore-of-a-read-write-file-full-recovery-model.md)을 참조하세요.  
  
     복사 전용 백업 이후에는 트랜잭션 로그를 자를 수 없습니다.  
  
 복사 전용 백업은 **backupset** 테이블의 [is_copy_only](/sql/relational-databases/system-tables/backupset-transact-sql) 열에 기록됩니다.  
  
## <a name="to-create-a-copy-only-backup"></a>복사 전용 백업을 만들려면  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../../includes/tsql-md.md)] 또는 PowerShell을 사용하여 복사 전용 백업을 만들 수 있습니다.  
  
###  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
1.  **데이터베이스 백업** 대화 상자의 **일반** 페이지에서 **복사 전용 백업** 옵션을 선택합니다.  
  
###  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 필수 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 구문은 다음과 같습니다.  
  
-   복사 전용 전체 백업의 경우:  
  
     데이터베이스를 \<backup_device *>* 에 백업 *database_name* ... COPY_ONLY 사용 ...  
  
    > [!NOTE]  
    >  DIFFERENTIAL 옵션과 함께 지정하면 COPY_ONLY가 적용되지 않습니다.  
  
-   복사 전용 로그 백업의 경우:  
  
     *\<* BACKUP_DEVICE *>* 백업 로그 *database_name* ... COPY_ONLY 사용 ...  
  
###  <a name="PowerShellProcedure"></a> PowerShell 사용  
  
`Backup-SqlDatabase` cmdlet을 `-CopyOnly` 매개 변수와 함께 사용합니다.  
  
##  <a name="RelatedTasks"></a> 관련 작업  

### <a name="to-create-a-full-or-log-backup"></a>전체 또는 로그 백업을 만들려면
  
-   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
### <a name="to-view-copy-only-backups"></a>복사 전용 백업을 보려면
  
-   [backupset&#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/backupset-transact-sql)  
  
### <a name="to-set-up-and-use-the-sql-server-powershell-provider"></a>SQL Server PowerShell 공급자를 설정하고 사용하려면
  
-   [SQL Server PowerShell 공급자](../../powershell/sql-server-powershell-provider.md)  

## <a name="see-also"></a>참고 항목  
 [백업 개요&#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [복구 모델&#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [백업 및 복원으로 데이터베이스 복사](../databases/copy-databases-with-backup-and-restore.md)   
 [복원 및 복구 개요&#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)  
