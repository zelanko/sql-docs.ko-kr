---
title: sys.dm_database_encryption_keys (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_database_encryption_keys
- sys.dm_database_encryption_keys_TSQL
- dm_database_encryption_keys
- dm_database_encryption_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_database_encryption_keys dynamic management view
ms.assetid: 56fee8f3-06eb-4fff-969e-abeaa0c4b8e4
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 880af4ca3aa53332791d2cfc26106f661e7c858f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmdatabaseencryptionkeys-transact-sql"></a>sys.dm_database_encryption_keys(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  연결된 데이터베이스 암호화 키 및 데이터베이스의 암호화 상태에 대한 정보를 반환합니다. 데이터 암호화에 대한 자세한 내용은 [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하십시오.  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|데이터베이스의 ID입니다.|  
|encryption_state|**int**|데이터베이스가 암호화되었는지 여부를 나타냅니다.<br /><br /> 0 = 데이터베이스 암호화 키가 없고 암호화되지 않음<br /><br /> 1 = 암호화되지 않음<br /><br /> 2 = 암호화 진행 중<br /><br /> 3 = 암호화됨<br /><br /> 4 = 키 변경 진행 중<br /><br /> 5 = 해독 진행 중<br /><br /> 6 = 보호 변경 진행 중. 데이터베이스 암호화 키를 암호화하는 인증서 또는 비대칭 키를 변경하고 있습니다.|  
|create_date|**datetime**|암호화 키를 만든 날짜를 표시합니다.|  
|regenerate_date|**datetime**|암호화 키를 다시 생성한 날짜를 표시합니다.|  
|modify_date|**datetime**|암호화 키를 수정한 날짜를 표시합니다.|  
|set_date|**datetime**|암호화 키가 데이터베이스에 적용된 날짜를 표시합니다.|  
|opened_date|**datetime**|데이터베이스 키가 마지막으로 열린 시간을 표시합니다.|  
|key_algorithm|**nvarchar(32)**|키에 사용된 알고리즘을 표시합니다.|  
|key_length|**int**|키의 길이를 표시합니다.|  
|encryptor_thumbprint|**varbinary(20)**|암호기의 손도장을 표시합니다.|  
|encryptor_type|**nvarchar(32)**|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).<br /><br /> 암호기를 설명합니다.|  
|percent_complete|**real**|데이터베이스 암호화 상태 변경의 완료 비율입니다. 상태 변경이 없으면 0이 됩니다.|  
  
## <a name="permissions"></a>Permissions

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요 `VIEW SERVER STATE` 권한.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요는 `VIEW DATABASE STATE` 데이터베이스에는 권한이 있습니다.   

## <a name="see-also"></a>관련 항목:  

 [보안 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [투명한 데이터 암호화&#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [SQL Server 암호화](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [SQL Server 및 데이터베이스 암호화 키&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  
