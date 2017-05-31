---
title: "SQL Server 2014 Managed Backup 설정을 SQL Server 2016으로 마이그레이션 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ae937ebb-24ff-4a33-be3c-8f85328dfc75
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 902ad2ddd95a26f36ff9519e55d7af77ca7e2d8a
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="migrate-sql-server-2014-managed-backup-settings-to-sql-server-2016"></a>SQL Server 2014 Managed Backup 설정을 SQL Server 2016으로 마이그레이션
  이 항목에서는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에서 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 으로 마이그레이션할 때의 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]관련 마이그레이션 고려 사항에 대해 설명합니다.  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에서는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 절차 및 기본 동작이 변경되었습니다. 다음 섹션에서는 기능 변경 내용 및 해당 의미에 대해 설명합니다.  
  
## <a name="overview"></a>개요  
 다음 표에서는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 와 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 에서 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 몇 가지 주요 기능 차이점에 대해 설명합니다.  
  
|영역|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|  
|----------|---------------------------|---------------------------|  
|**네임스페이스:**|smart_admin|managed_backup|  
|**시스템 저장 프로시저:**|sp_set_db_backup<br /><br /> sp_set_instance_backup|[managed_backup.sp_backup_config_basic(Transact-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)<br /><br /> [sp_backup_config_advanced](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-advanced-transact-sql.md)<br /><br /> [sp_backup_config_schedule](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)|  
|**보안:**|Microsoft Azure Storage 계정 및 액세스 키를 사용하는 SQL 자격 증명|Microsoft Azure SAS(공유 액세스 서명) 토큰을 사용하는 SQL 자격 증명|  
|**기본 저장소:**|페이지 Blob을 사용하는 Microsoft Azure Storage|블록 Blob을 사용하는 Microsoft Azure Storage|  
  
## <a name="benefits"></a>이점  
 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 새로운 기능을 사용하는 경우 다음과 같은 여러 이점이 제공됩니다.  
  
-   블록 Blob에서는 저장소 비용이 더 적게 듭니다.  
  
-   스트라이핑 기능을 사용하면 훨씬 큰 백업(12TB/페이지 Blob의 경우 1TB)을 저장할 수 있습니다.  
  
-   또한 스트라이핑을 수행하면 큰 데이터베이스의 복원 시간도 단축할 수 있습니다.  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에서 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]의 기타 개선 사항은 [Microsoft Azure에 대한 SQL Server Managed Backup](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)을 참조하세요.  
  
## <a name="considerations"></a>고려 사항  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 업그레이드한 후에는 다음과 같은 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 관련 사항을 고려하세요.  
  
-   [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 에서 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 용으로 이전에 구성한 모든 데이터베이스는 **에서도** smart_admin [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]시스템 프로시저 및 기본 동작을 계속 사용합니다.  
  
-   **에서** 의 새 구성에는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] smart_admin [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]프로시저가 지원되지 않습니다. 따라서 새 **managed_backup** 프로시저와 기능을 사용해야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft Azure에 대한 SQL Server Managed Backup](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
