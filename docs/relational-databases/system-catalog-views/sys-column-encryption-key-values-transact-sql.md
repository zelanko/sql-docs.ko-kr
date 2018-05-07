---
title: sys.column_encryption_key_values (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
f1_keywords:
- column_encryption_key_values
- column_encryption_key_values_TSQL
- sys.column_encryption_key_values
- sys.column_encryption_key_values_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_encryption_key_values catalog view
ms.assetid: 440875ab-b0e9-4966-8c16-01503558fedd
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 02d0ce79355422943b21608d546890ebd1bc61e0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="syscolumnencryptionkeyvalues-transact-sql"></a>sys.column_encryption_key_values (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  암호화 키 (Cek) 중 하나를 사용 하 여 만든 열의 암호화 된 값에 대 한 정보를 반환 합니다.는 [CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) 또는 [ALTER COLUMN ENCRYPTION KEY &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)문입니다. 각 행의 열 마스터 키 (CMK)로 암호화 된 CEK 값을 나타냅니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_id**|**int**|CEK는 데이터베이스에서의 ID입니다.|  
|**column_master_key_id**|**int**|CEK 값을 암호화 하는 데 사용 된 열 마스터 키의 ID입니다.|  
|**encrypted_value**|**varbinary(8000)**|Column_master_key_id에 지정 된 CMK로 암호화 된 CEK 값입니다.|  
|**encryption_algorithm_name**|**sysname**|CEK 값을 암호화 하는 데 사용 되는 알고리즘의 이름입니다.<br /><br /> 값을 암호화하는 데 사용되는 암호화 알고리즘의 이름입니다. 시스템 공급자에 대 한 알고리즘 해야 **RSA_OAEP**합니다.|  
  
## <a name="permissions"></a>Permissions  
 필요는 **VIEW ANY COLUMN ENCRYPTION KEY** 권한.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE COLUMN ENCRYPTION KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_keys&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_master_keys&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
  
