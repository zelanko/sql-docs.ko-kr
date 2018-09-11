---
title: ALTER DATABASE ENCRYPTION KEY(Transact-SQL) | Microsoft Docs
ms.date: 04/16/2018
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_ENCRYPTION_KEY_TSQL
- ALTER DATABASE ENCRYPTION
- ALTER_DATABASE_ENCRYPTION_TSQL
- ALTER DATABASE ENCRYPTION KEY
dev_langs:
- TSQL
helpviewer_keywords:
- database encryption key, alter
- ALTER DATABASE ENCRYPTION KEY
ms.assetid: f88dac4b-efe0-47ed-9808-972a4381377e
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 2ec636ee6d5aa92fa6dca7454f100d2fd7ef0134
ms.sourcegitcommit: 8ae6e6618a7e9186aab3c6a37ea43776aa9a382b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43814839"
---
# <a name="alter-database-encryption-key-transact-sql"></a>ALTER DATABASE ENCRYPTION KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  데이터베이스를 명시적으로 암호화하는 데 사용되는 암호화 키와 인증서를 변경합니다. TDE(투명한 데이터 암호화)에 대한 자세한 내용은 [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하십시오.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
-- Syntax for SQL Server  
  
ALTER DATABASE ENCRYPTION KEY  
      REGENERATE WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
   |  
   ENCRYPTION BY SERVER   
    {  
        CERTIFICATE Encryptor_Name |  
        ASYMMETRIC KEY Encryptor_Name  
    }  
[ ; ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
ALTER DATABASE ENCRYPTION KEY  
    {  
      {  
        REGENERATE WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
        [ ENCRYPTION BY SERVER CERTIFICATE Encryptor_Name ]  
      }  
      |  
      ENCRYPTION BY SERVER   CERTIFICATE Encryptor_Name    
    }  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 REGENERATE WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
 암호화 키에 사용되는 암호화 알고리즘을 지정합니다.  
  
 ENCRYPTION BY SERVER CERTIFICATE *Encryptor_Name*  
 데이터베이스 암호화 키를 암호화하는 데 사용되는 인증서의 이름을 지정합니다.  
  
 ENCRYPTION BY SERVER ASYMMETRIC KEY Encryptor_Name  
 데이터베이스 암호화 키를 암호화하는 데 사용되는 비대칭 키의 이름을 지정합니다.  
  
## <a name="remarks"></a>Remarks  
 데이터베이스 암호화 키를 암호화하는 데 사용되는 인증서 또는 비대칭 키는 master 시스템 데이터베이스에 있어야 합니다.  
  
 Dbo(데이터베이스 소유자)가 변경될 경우 데이터베이스 암호화 키를 다시 생성하지 않아도 됩니다.
  
 데이터베이스 암호화 키를 두 번 수정한 후 다시 데이터베이스 암호화 키를 수정하려면 먼저 로그 백업을 수행해야 합니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 CONTROL 권한과 데이터베이스 암호화 키를 암호화하는 데 사용되는 인증서 또는 비대칭 키에 대한 VIEW DEFINITION 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 `AES_256` 알고리즘을 사용하여 데이터베이스 암호화 키를 변경합니다.  
  
```  
-- Uses AdventureWorks  
  
ALTER DATABASE ENCRYPTION KEY  
REGENERATE WITH ALGORITHM = AES_256;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [투명한 데이터 암호화&#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [SQL Server 암호화](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [SQL Server 및 데이터베이스 암호화 키&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)   
 [sys.dm_database_encryption_keys&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)  
  
  

