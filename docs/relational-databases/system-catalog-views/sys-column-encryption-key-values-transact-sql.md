---
title: sys.column_encryption_key_values (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
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
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2c4a9f214ca9a947e8f488dd347f69b487b963e3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68140116"
---
# <a name="syscolumnencryptionkeyvalues-transact-sql"></a>sys.column_encryption_key_values (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  암호화 키 (CEKs)을 사용 하 여 만들 열 암호화 된 값에 대 한 정보를 반환 하면 [열 암호화 키 만들기](../../t-sql/statements/create-column-encryption-key-transact-sql.md) 또는 [열 암호화 키 변경 &#40;Transact SQL&#41; ](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)문. 각 행의 열 (CMK) 마스터 키로 암호화 하 여 CEK 값을 나타냅니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_id**|**int**|데이터베이스에 CEK의 ID입니다.|  
|**column_master_key_id**|**int**|CEK 값을 암호화 하는 데 사용 된 열 마스터 키의 ID입니다.|  
|**encrypted_value**|**varbinary(8000)**|Column_master_key_id에 지정 된 CMK로 암호화 된 CEK 값입니다.|  
|**encryption_algorithm_name**|**sysname**|CEK 값을 암호화 하는 데 사용 되는 알고리즘의 이름입니다.<br /><br /> 값을 암호화하는 데 사용되는 암호화 알고리즘의 이름입니다. 시스템 공급자에 대 한 알고리즘 이어야 합니다 **RSA_OAEP**합니다.|  
  
## <a name="permissions"></a>사용 권한  
 필요 하면 **모든 열 암호화 키 보기** 권한.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [CREATE COLUMN ENCRYPTION KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [DROP COLUMN ENCRYPTION KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.column_encryption_keys&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [sys.column_master_keys&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
 [sys.columns&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
  
