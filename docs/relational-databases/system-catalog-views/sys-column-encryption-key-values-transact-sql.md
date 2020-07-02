---
title: sys. column_encryption_key_values (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
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
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c9c17ef0384d1b4ef1bc5534ffeffa8b2ba3d598
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718888"
---
# <a name="syscolumn_encryption_key_values-transact-sql"></a>sys. column_encryption_key_values (Transact-sql)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [CREATE COLUMN ENCRYPTION key](../../t-sql/statements/create-column-encryption-key-transact-sql.md) 또는 [ALTER column Encryption key &#40;transact-sql&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md) 문으로 만든 ceks (열 암호화 키)의 암호화 된 값에 대 한 정보를 반환 합니다. 각 행은 CMK (열 마스터 키)로 암호화 된 CEK의 값을 나타냅니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_id**|**int**|데이터베이스에 있는 CEK의 ID입니다.|  
|**column_master_key_id**|**int**|CEK 값을 암호화 하는 데 사용 된 열 마스터 키의 ID입니다.|  
|**encrypted_value**|**varbinary(8000)**|Column_master_key_id에 지정 된 CMK로 암호화 된 CEK 값입니다.|  
|**encryption_algorithm_name**|**sysname**|CEK 값을 암호화 하는 데 사용 되는 알고리즘의 이름입니다.<br /><br /> 값을 암호화하는 데 사용되는 암호화 알고리즘의 이름입니다. 시스템 공급자의 알고리즘은 **RSA_OAEP**해야 합니다.|  
  
## <a name="permissions"></a>사용 권한  
 **VIEW ANY COLUMN ENCRYPTION KEY** 권한이 필요 합니다.  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;열 암호화 키 만들기](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [Transact-sql&#41;&#40;열 암호화 키 변경](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [Transact-sql&#41;&#40;열 암호화 키 삭제](../../t-sql/statements/drop-column-encryption-key-transact-sql.md)   
 [Transact-sql&#41;&#40;열 마스터 키 만들기](../../t-sql/statements/create-column-master-key-transact-sql.md)   
 [Transact-sql&#41;&#40;보안 카탈로그 뷰](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [column_encryption_keys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)   
 [column_master_keys &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)   
 [&#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Secure enclaves를 사용 하는 Always Encrypted](../../relational-databases/security/encryption/always-encrypted-enclaves.md)   
 [Always Encrypted 키 관리 개요](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)   
 [보안 Enclave를 사용한 Always Encrypted 키 관리](../../relational-databases/security/encryption/always-encrypted-enclaves-manage-keys.md)   

  
  
