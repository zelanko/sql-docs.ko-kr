---
title: managed_backup.sp_backup_config_advanced (TRANSACT-SQL) | Microsoft Docs
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c3f19fed072e693de6bbebb53354eae8c0bfaa0e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47827911"
---
# <a name="managedbackupspbackupconfigadvanced-transact-sql"></a>managed_backup.sp_backup_config_advanced (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  에 대 한 고급 설정을 구성 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```vb  
EXEC managed_backup.sp_backup_config_advanced   
    [@database_name = ] 'database_name'  
    ,[@encryption_algorithm = ] 'name of the encryption algorithm'  
    ,[@encryptor_type = ] {'CERTIFICATE' | 'ASYMMETRIC_KEY'}  
    ,[@encryptor_name = ] 'name of the certificate or asymmetric key'  
    ,[@local_cache_path = ] 'NOT AVAILABLE'  
```  
  
##  <a name="Arguments"></a> 인수  
 @database_name  
 특정 데이터베이스에 대 한 managed backup을 사용 하도록 설정 하는 것에 대 한 데이터베이스 이름입니다. Null 인 경우 또는 *, 관리 되는 backup이 서버의 모든 데이터베이스에 적용 됩니다.  
  
 @encryption_algorithm  
 백업 중에 백업 파일을 암호화하는 데 사용되는 암호화 알고리즘의 이름입니다. 합니다 @encryption_algorithm 됩니다 **SYSNAME**합니다. 데이터베이스에 대해 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)]을 처음으로 구성할 경우 필수 매개 변수입니다. 지정할 **NO_ENCRYPTION** 백업 파일을 암호화 하 고 싶지 않은 경우. [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] 구성 설정을 변경하는 경우 이 매개 변수는 선택 사항이며 매개 변수가 지정되지 않는 경우 기존 구성 값이 유지됩니다. 이 매개 변수의 허용되는 값은 다음과 같습니다.  
  
-   AES_128  
  
-   AES_192  
  
-   AES_256  
  
-   TRIPLE_DES_3KEY  
  
-   NO_ENCRYPTION  
  
 암호화 알고리즘에 대한 자세한 내용은 [Choose an Encryption Algorithm](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)을 참조하세요.  
  
 @encryptor_type  
 'CERTIFICATE' 수 있는 암호기의 형식 또는 ' ASYMMETRIC_KEY "입니다. 합니다 @encryptor_type 됩니다 **nvarchar(32)** 합니다. 이 매개 변수는 선택 사항에 대해 NO_ENCRYPTION을 지정한 경우는 @encryption_algorithm 매개 변수입니다.  
  
 @encryptor_name  
 백업 암호화에 사용되는 비대칭 키 또는 기존 인증서의 이름입니다. 합니다 @encryptor_name 됩니다 **SYSNAME**합니다. 비대칭 키를 사용하는 경우 EKM(확장 키 관리)와 함께 구성해야 합니다. 이 매개 변수는 선택 사항에 대해 NO_ENCRYPTION을 지정한 경우는 @encryption_algorithm 매개 변수입니다.  
  
 자세한 내용은 [EKM&#40;확장 가능 키 관리&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)을 참조하세요.  
  
 @local_cache_path  
 이 매개 변수는 아직 지원 되지 않습니다.  
  
## <a name="return-code-value"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 **db_backupoperator** 사용 하 여 데이터베이스 역할 **ALTER ANY CREDENTIAL** 권한 및 **EXECUTE** 에 대 한 권한을 **sp_delete_ backuphistory** 저장 프로시저입니다.  
  
## <a name="examples"></a>예  
 에 대 한 고급 구성 옵션을 설정 하는 다음 예제에서는 [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] SQL Server 인스턴스에 대 한 합니다.  
  
```  
Use msdb;  
Go  
   EXEC managed_backup.sp_backup_config_advanced  
                @encryption_algorithm ='AES_128'  
                ,@encryptor_type = 'CERTIFICATE'  
                ,@encryptor_name = 'MyTestDBBackupEncryptCert'  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [managed_backup.sp_backup_config_basic (TRANSACT-SQL)](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-basic-transact-sql.md)   
 [managed_backup.sp_backup_config_schedule&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/managed-backup-sp-backup-config-schedule-transact-sql.md)  
  
  
