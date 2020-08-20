---
description: managed_backup. sp_backup_master_switch (Transact-sql)
title: managed_backup. sp_backup_master_switch (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_ backup_master_switch
- smart_admin.sp_backup_master_switch
- sp_ backup_master_switch_TSQL
- smart_admin.sp_backup_master_switch_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_ backup_master_switch
- smart_admin.sp_backup_master_switch
ms.assetid: 1ed2b2b2-c897-41cc-bed5-1c6bc47b9dd2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 193125f68cb5282e2aece4b00a3d41e1d3690464
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454771"
---
# <a name="managed_backupsp_backup_master_switch-transact-sql"></a>managed_backup. sp_backup_master_switch (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 일시 중지하거나 다시 시작합니다.  
  
 이 저장 프로시저를 사용하여 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 일시 중지하고 다시 시작할 수 있습니다. 이는 작업이 다시 시작될 때 모든 구성 설정이 그대로 보존되도록 합니다. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]이 일시 중지되면 보존 기간이 적용되지 않습니다. 이는 파일이 스토리지에서 삭제되었는지 여부 또는 백업 파일이 손상되었거나 로그 체인이 끊어졌는지를 확인하기 위한 점검이 없음을 의미합니다.  
  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
EXEC managed_backup.sp_backup_master_switch   
                     [@new_state = ] { 0 | 1}  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 인수  
 @state  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]의 상태를 설정합니다. @state매개 변수가 **비트**입니다. 값을 0으로 설정하면 작업이 일시 중지되고 1로 설정하면 작업이 다시 시작됩니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="security"></a>보안  
 하위 섹션(H3 머리글)에서 statement.Include 사용 권한과 관련된 보안 문제를 설명합니다. 해당되는 경우 소유권 체인 및 감사에 대한 다른 하위 섹션을 포함하는 것을 고려해 보세요.  
  
### <a name="permissions"></a>사용 권한  
 **ALTER ANY CREDENTIAL** 권한 및 **sp_delete_backuphistory**저장 프로시저에 대 한 **EXECUTE** 권한이 있는 **db_backupoperator** 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예제  
 인스턴스에서 실행 중인 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 일시 중지하는 데 다음 예를 사용할 수 있습니다.  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_backup_master_switch @new_state=0;  
Go  
  
```  
  
 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 다시 시작하는 데 다음 예를 사용할 수 있습니다.  
  
```  
Use msdb;  
GO  
EXEC managed_backup.sp_backup_master_switch @new_state=1;  
Go  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft Azure에 SQL Server Managed Backup](../../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)  
  
  
