---
title: CREATE DATABASE ENCRYPTION KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DATABASE_ENCRYPTION_KEY_TSQL
- ENCRYPTION_KEY_TSQL
- sql13.swb.dbencryptionkeyo.f1
- ENCRYPTION KEY
- DATABASE ENCRYPTION KEY
- CREATE_DATABASE_ENCRYPTION_KEY_TSQL
- CREATE DATABASE ENCRYPTION KEY
- sql13.swb.dbencryptionkeyg.f1
- CREATE DATABASE ENCRYPTION
- CREATE_DATABASE_ENCRYPTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database encryption key
- CREATE DATABASE ENCRYPTION KEY statement
- database encryption key, create
ms.assetid: 2ee95a32-5140-41bd-9ab3-a947b9990688
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6ae0dcf565b5798c5a4e94339f9d6382deb94e8c
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81633257"
---
# <a name="create-database-encryption-key-transact-sql"></a>CREATE DATABASE ENCRYPTION KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

 데이터베이스를 명시적으로 암호화하는 데 사용되는 암호화 키를 만듭니다. TDE(투명한 데이터 암호화)에 대한 자세한 내용은 [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하십시오.  
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
-- Syntax for SQL Server  

CREATE DATABASE ENCRYPTION KEY  
       WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
   ENCRYPTION BY SERVER   
    {  
        CERTIFICATE Encryptor_Name |  
        ASYMMETRIC KEY Encryptor_Name  
    }  
[ ; ]  
```  
  
```syntaxsql
-- Syntax for Parallel Data Warehouse  

CREATE DATABASE ENCRYPTION KEY  
       WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY }  
   ENCRYPTION BY SERVER CERTIFICATE Encryptor_Name   
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
WITH ALGORITHM = { AES_128 | AES_192 | AES_256 | TRIPLE_DES_3KEY  }  
암호화 키에 사용되는 암호화 알고리즘을 지정합니다.   
> [!NOTE]
>    SQL Server 2016부터는 AES_128, AES_192 및 AES_256 이외의 모든 알고리즘을 지원하지 않습니다. 오래된 알고리즘을 사용하려면(권장하지 않음) 데이터베이스 호환성 수준을 120 이하로 설정해야 합니다.  
  
ENCRYPTION BY SERVER CERTIFICATE Encryptor_Name  
데이터베이스 암호화 키를 암호화하는 데 사용되는 암호기의 이름을 지정합니다.  
  
ENCRYPTION BY SERVER ASYMMETRIC KEY Encryptor_Name  
데이터베이스 암호화 키를 암호화하는 데 사용되는 비대칭 키의 이름을 지정합니다. 비대칭 키로 데이터베이스 암호화 키를 암호화하려면 비대칭 키가 확장 가능 키 관리 공급자에 있어야 합니다.  
  
## <a name="remarks"></a>설명  
데이터베이스 암호화 키가 있어야 TDE(*Transparent Database Encryption*)를 사용하여 데이터베이스를 암호화할 수 있습니다. 데이터베이스가 명시적으로 암호화되면 특수 코드의 수정 없이 전체 데이터베이스가 파일 수준에서 암호화됩니다. 데이터베이스 암호화 키를 암호화하는 데 사용되는 인증서 또는 비대칭 키는 master 시스템 데이터베이스에 있어야 합니다.  
  
데이터베이스 암호화 문은 사용자 데이터베이스에서만 사용할 수 있습니다.  
  
데이터베이스 암호화 키는 데이터베이스에서 내보낼 수 없습니다. 이 작업은 해당 시스템, 서버에서 디버깅 권한이 있는 사용자, 데이터베이스 암호화 키를 암호화하고 해독하는 인증서에 액세스할 수 있는 사용자만 수행할 수 있습니다.  
  
Dbo(데이터베이스 소유자)가 변경될 경우 데이터베이스 암호화 키를 다시 생성하지 않아도 됩니다.  
  
데이터베이스 암호화 키는 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 데이터베이스에 대해 자동으로 생성됩니다. CREATE DATABASE ENCRYPTION KEY 문을 사용하여 키를 만들 필요가 없습니다.  
  
## <a name="permissions"></a>사용 권한  
데이터베이스에 대한 CONTROL 권한과 데이터베이스 암호화 키를 암호화하는 데 사용되는 인증서 또는 비대칭 키에 대한 VIEW DEFINITION 권한이 필요합니다.  
  
## <a name="examples"></a>예  
TDE를 사용하는 추가 예제를 보려면 [투명한 데이터 암호화 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md), [EKM을 사용하여 SQL Server에서 TDE를 사용하도록 설정](../../relational-databases/security/encryption/enable-tde-on-sql-server-using-ekm.md) 및 [Azure Key Vault를 사용한 확장 가능 키 관리 &#40;SQL Server&#41;](../../relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md)를 참조하세요.  
  
다음 예에서는 `AES_256` 알고리즘을 사용하여 데이터베이스 암호화 키를 만들고 `MyServerCert`라는 인증서로 프라이빗 키를 보호합니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE DATABASE ENCRYPTION KEY  
WITH ALGORITHM = AES_256  
ENCRYPTION BY SERVER CERTIFICATE MyServerCert;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
[투명한 데이터 암호화&#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
[SQL Server 암호화](../../relational-databases/security/encryption/sql-server-encryption.md)   
[SQL Server 및 데이터베이스 암호화 키&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
[암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
[ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
[ALTER DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
[DROP DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)   
[sys.dm_database_encryption_keys&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql.md)  
    
