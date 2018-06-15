---
title: managed_backup.fn_backup_instance_config (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_backup_instance_config
- smart_admin.fn_backup_instance_config_TSQL
- fn_backup_instance_config_TSQL
- smart_admin.fn_backup_instance_config
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_backup_instance_config
- fn_backup_instance_config
ms.assetid: 2382a547-c0c9-4e1d-87c9-d8526192eb5a
caps.latest.revision: 16
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4dae80911e6508a1a398cf208300bf4145faeecc
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33229998"
---
# <a name="managedbackupfnbackupinstanceconfig-transact-sql"></a>managed_backup.fn_backup_instance_config (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  SQL Server 인스턴스에 대한 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 기본 구성 설정이 포함된 행을 하나 반환합니다.  
  
 이 저장 프로시저를 사용하여 SQL Server 인스턴스에 대한 현재 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 기본 구성 설정을 검토하거나 확인할 수 있습니다.  
  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
managed_backup.fn_backup_db_config ()  
```  
  
##  <a name="Arguments"></a> 인수  
 InclusionThresholdSetting  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|is_smart_backup_enabled|INT|[!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]이 설정되었으면 1을 표시하고, [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]이 해제되었으면 0을 표시합니다.|  
|credential_name|SYSNAME|저장소 계정 인증에 사용되는 기본 SQL 자격 증명입니다.|  
|retention_days|INT|인스턴스 수준에서 설정된 기본 보존 기간입니다.|  
|storage_url|NVARCHAR (1024)|인스턴스 수준에서 설정된 기본 저장소 계정 URL입니다.|  
|encryption_algorithm|SYSNAME|암호화 알고리즘의 이름입니다. 암호화가 지정되지 않은 경우 NULL로 설정됩니다.|  
|encryptor_type|NVARCHAR (32)|사용한 암호기 유형: 인증서 또는 비대칭 키입니다. 암호기가 지정되지 않은 경우 NULL로 설정됩니다.|  
|encryptor_name|SYSNAME|인증서 또는 비대칭 키의 이름입니다. 이름이 지정되지 않은 경우 NULL로 설정됩니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **db_backupoperator** 데이터베이스 역할 **ALTER ANY CREDENTIAL** 사용 권한. 사용자를 거부 되어서는 안 **VIEW ANY DEFINITION** 사용 권한.  
  
## <a name="examples"></a>예  
 다음 예에서는 코드가 실행되는 인스턴스에 대한 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 기본 구성 설정을 반환합니다.  
  
```  
Use msdb;  
GO  
SELECT * FROM managed_backup.fn_backup_instance_config ();  
  
```  
  
  
