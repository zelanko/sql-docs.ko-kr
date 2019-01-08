---
title: managed_backup.sp_backup_on_demand (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- smart_admin.sp_backup_on_demand
- smart_admin.sp_backup_on_demand_TSQL
- sp_backup_on_demand_TSQL
- sp_backup_on_demand
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.sp_backup_on_demand
- sp_backup_on_demand
ms.assetid: 638f809f-27fa-4c44-a549-9cf37ecc920c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8945ba72471855b2c3de5b169b12bea4cc2b656e
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52391348"
---
# <a name="managedbackupspbackupondemand-transact-sql"></a>managed_backup.sp_backup_on_demand (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  지정된 데이터베이스 백업을 수행하려면 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 요청합니다.  
  
 이 저장 프로시저를 사용하면 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]으로 구성된 데이터베이스에 대한 임시 백업을 수행할 수 있습니다. 이렇게 하면 백업 체인이 끊어지는 것을 방지하고 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 프로세스를 인지할 수 있으며, 백업이 동일한 Windows Azure Blob 저장소 컨테이너에 저장됩니다.  
  
 백업이 성공적으로 완료된 다음에는 전체 백업 파일 경로가 반환됩니다. 여기에는 백업 작업으로 발생하는 새 백업 파일의 이름 및 위치가 포함됩니다.  
  
 지정된 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]이 지정된 유형의 백업을 실행하는 중에 있으면 오류가 반환됩니다. 이 경우 반환된 오류 메시지에는 현재 백업을 업그레이드 중인 전체 백업 파일 경로가 포함됩니다.  
   
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
EXEC managed_backup.sp_backup_on_demand   
[@database_name  =]  'database name',[@type = ] { 'Database' | 'Log' }  
  
```  
  
##  <a name="Arguments"></a> 인수  
 @database_name  
 백업을 수행할 데이터베이스의 이름입니다. 합니다 @database_name 됩니다 **SYSNAME**합니다.  
  
 @type  
 수행할 백업 유형으로서,  데이터베이스 또는 로그입니다. 합니다 @type 매개 변수가 **NVARCHAR(32)** 합니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 **db_backupoperator** 사용 하 여 데이터베이스 역할 **ALTER ANY CREDENTIAL** 권한 및 **EXECUTE** 에 대 한 권한을 **sp_delete_ backuphistory**저장 프로시저입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 'TestDB' 데이터베이스에 대 한 데이터베이스 백업 요청을 합니다. 이 데이터베이스에는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]이 설정되어 있습니다.  
  
```  
Use MSDB  
Go  
EXEC managed_backup.sp_backup_on_demand  
 @database_name = 'TestDB'  
,@type = 'Database'  
  
```  
  
 각 코드 조각에 대해 언어 특성 필드에서 'tsql'을 선택합니다.  
  
  
