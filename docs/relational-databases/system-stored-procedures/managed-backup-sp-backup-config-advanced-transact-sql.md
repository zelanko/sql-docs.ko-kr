---
description: managed_backup. sp_backup_config_advanced (Transact-sql)
title: managed_backup. sp_backup_config_advanced (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_backup_config_optional
- sp_backup_config_optional_TSQL
- managed_backup.sp_backup_config_optional_TSQL
- managed_backup.sp_backup_config_optional
dev_langs:
- TSQL
helpviewer_keywords:
- sp_backup_config_optional
- managed_backup.sp_backup_config_optional
ms.assetid: 4fae8193-1f88-48fd-a94a-4786efe8d6af
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d092851d710de96e9c1b06d2866183a7dfac01bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464695"
---
# <a name="managed_backupsp_backup_config_advanced-transact-sql"></a>managed_backup. sp_backup_config_advanced (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  에 대 한 고급 설정을 구성 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
EXEC managed_backup.sp_backup_config_advanced   
    [@database_name = ] 'database_name'  
    ,[@encryption_algorithm = ] 'name of the encryption algorithm'  
    ,[@encryptor_type = ] {'CERTIFICATE' | 'ASYMMETRIC_KEY'}  
    ,[@encryptor_name = ] 'name of the certificate or asymmetric key'  
    ,[@local_cache_path = ] 'NOT AVAILABLE'  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> 인수  
 @database_name  
 특정 데이터베이스에서 관리 되는 백업을 사용 하도록 설정 하기 위한 데이터베이스 이름입니다. NULL 또는 * 인 경우이 관리 되는 백업은 서버의 모든 데이터베이스에 적용 됩니다.  
  
 @encryption_algorithm  
 백업 중에 백업 파일을 암호화하는 데 사용되는 암호화 알고리즘의 이름입니다. 는 @encryption_algorithm **SYSNAME**입니다. 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 처음으로 구성할 경우 필수 매개 변수입니다. 백업 파일을 암호화 하지 않으려면 **NO_ENCRYPTION** 를 지정 합니다. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]구성 설정을 변경 하는 경우이 매개 변수는 선택 사항입니다. 매개 변수를 지정 하지 않으면 기존 구성 값이 유지 됩니다. 이 매개 변수의 허용되는 값은 다음과 같습니다.  
  
-   AES_128  
  
-   AES_192  
  
-   AES_256  
  
-   TRIPLE_DES_3KEY  
  
-   NO_ENCRYPTION  
  
 암호화 알고리즘에 대한 자세한 내용은 [Choose an Encryption Algorithm](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)을 참조하세요.  
  
 @encryptor_type  
 ' CERTIFICATE ' 또는 ' ASYMMETRIC_KEY "일 수 있는 암호기의 유형입니다. 는 @encryptor_type **nvarchar (32)** 입니다. 매개 변수에 대 한 NO_ENCRYPTION 지정 하는 경우이 매개 변수는 선택 사항입니다 @encryption_algorithm .  
  
 @encryptor_name  
 백업 암호화에 사용되는 비대칭 키 또는 기존 인증서의 이름입니다. 는 @encryptor_name **SYSNAME**입니다. 비대칭 키를 사용하는 경우 EKM(확장 키 관리)와 함께 구성해야 합니다. 매개 변수에 대 한 NO_ENCRYPTION 지정 하는 경우이 매개 변수는 선택 사항입니다 @encryption_algorithm .  
  
 자세한 내용은 [EKM&#41;&#40;확장 가능 키 관리 ](../../relational-databases/security/encryption/extensible-key-management-ekm.md)를 참조 하세요.  
  
 @local_cache_path  
 이 매개 변수는 아직 지원 되지 않습니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 **ALTER ANY CREDENTIAL** 권한 및 **sp_delete_backuphistory** 저장 프로시저에 대 한 **EXECUTE** 권한이 있는 **db_backupoperator** 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 SQL Server 인스턴스에 대 한 고급 구성 옵션을 설정 합니다 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] .  
  
```sql
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_advanced  
                @encryption_algorithm ='AES_128'  
                ,@encryptor_type = 'CERTIFICATE'  
                ,@encryptor_name = 'MyTestDBBackupEncryptCert'  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [managed_backup. sp_backup_config_basic (Transact-sql)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
