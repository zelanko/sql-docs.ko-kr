---
title: managed_backup. fn_backup_db_config (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- smart_admin.fn_backup_db_config
- smart_admin.fn_backup_db_config_TSQL
- fn_backup_db_config
- fn_backup_db_config_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- smart_admin.fn_backup_db_config
- fn_backup_db_config
ms.assetid: 7c755d8a-64dd-44b2-be5e-735d30758900
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: a23f8eb64ae99b999cdf6b16f1c888383a88c147
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68067785"
---
# <a name="managed_backupfn_backup_db_config-transact-sql"></a>managed_backup. fn_backup_db_config (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  
  [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 구성 설정으로 0개, 1개 또는 그 이상의 행을 반환합니다. 지정된 데이터베이스에 대한 1개 행을 반환하거나 인스턴스에서 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 사용하여 구성된 모든 데이터베이스에 대한 정보를 반환합니다.  
  
 이 저장 프로시저를 사용하면 SQL Server 인스턴스에 있는 하나의 데이터베이스 또는 모든 데이터베이스에 대해 현재 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 구성 설정을 검토 또는 확인할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
managed_backup.fn_backup_db_config ('database_name' | '' | NULL)  
```  
  
##  <a name="Arguments"></a> 인수  
 @db_name  
 데이터베이스의 이름입니다. 매개 @db_name 변수는 **SYSNAME**입니다. 빈 문자열 또는 NULL 값이 이 매개 변수에 전달되면 SQL Server 인스턴스의 모든 데이터베이스에 대한 정보가 반환됩니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|db_name|SYSNAME|데이터베이스 이름|  
|db_guid|UNIQUEIDENTIFIER|데이터베이스를 고유하게 식별하는 식별자입니다.|  
|is_availability_database|BIT|데이터베이스가 가용성 그룹에 참여 중인지 여부입니다. 값 1은 데이터베이스가 가용성 데이터베이스임을 나타내고 0은 그렇지 않음을 나타냅니다.|  
|is_dropped|BIT|값 1은 삭제된 데이터베이스임을 나타냅니다.|  
|credential_name|SYSNAME|스토리지 계정 인증에 사용되는 SQL 자격 증명의 이름입니다. NULL 값은 SQL 자격 증명이 설정되지 않았음을 나타냅니다.|  
|retention_days|INT|현재 보존 기간(일)입니다. NULL 값은 이 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]이 구성되지 않았음을 나타냅니다.|  
|is_managed_backup_enabled|INT|이 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]이 현재 사용하도록 설정되었는지 여부를 나타냅니다. 값 1은 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]이 현재 사용하도록 설정되었음을 나타내고 값 0은 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]이 이 데이터베이스에 대해 사용하도록 설정되지 않았음을 나타냅니다.|  
|storage_url|NVARCHAR (1024)|스토리지 계정의 URL입니다.|  
|Encryption_algorithm|NCHAR (20)|백업을 암호화할 때 사용할 현재 암호화 알고리즘을 반환합니다.|  
|Encryptor_type|NCHAR(15)|암호기 설정: 인증서 또는 비대칭 키를 반환 합니다.|  
|Encryptor_name|NCHAR(max_length_of_cert/asymm_key_name)|인증서 또는 비대칭 키의 이름입니다.|  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 **ALTER ANY CREDENTIAL** 권한이 있는 **db_backupoperator** 데이터베이스 역할의 멤버 자격이 필요 합니다. 사용자에 게 **VIEW ANY DEFINITION** 권한이 거부 되어서는 안 됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 ' TestDB '에 대 한 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 구성을 반환 합니다.  
  
 각 코드 조각에 대해 언어 특성 필드에서 'tsql'을 선택합니다.  
  
```  
Use msdb  
GO  
SELECT * FROM managed_backup.fn_backup_db_config('TestDB')  
```  
  
 다음 예에서는 코드가 실행되는 SQL Server 인스턴스에서 모든 데이터베이스에 대한 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 구성을 반환합니다.  
  
```  
Use msdb  
GO  
SELECT * FROM managed_backup.fn_backup_db_config (NULL)  
```  
  
  
