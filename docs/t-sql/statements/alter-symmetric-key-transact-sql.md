---
title: ALTER SYMMETRIC KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER SYMMETRIC KEY
- ALTER_SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- modifying symmetric keys
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], modifying
- cryptography [SQL Server], symmetric keys
- ALTER SYMMETRIC KEY statement
ms.assetid: d3c776a4-7d71-4e6f-84fc-1db47400c465
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7314659cc8d0ba18b5b7b7b562ad5df467988638
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68070248"
---
# <a name="alter-symmetric-key-transact-sql"></a>ALTER SYMMETRIC KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  대칭 키의 속성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER SYMMETRIC KEY Key_name <alter_option>  
  
<alter_option> ::=  
   ADD ENCRYPTION BY <encrypting_mechanism> [ , ... n ]  
   |   
   DROP ENCRYPTION BY <encrypting_mechanism> [ , ... n ]  
<encrypting_mechanism> ::=  
   CERTIFICATE certificate_name  
   |  
   PASSWORD = 'password'  
   |  
   SYMMETRIC KEY Symmetric_Key_Name  
   |  
   ASYMMETRIC KEY Asym_Key_Name  
```  
  
## <a name="arguments"></a>인수  
 *Key_name*  
 데이터베이스에서 변경할 대칭 키를 식별하는 이름입니다.  
  
 ADD ENCRYPTION BY  
 지정된 방법을 사용하여 암호화를 추가합니다.  
  
 DROP ENCRYPTION BY  
 지정된 방법의 암호화를 삭제합니다. 대칭 키의 암호화를 모두 제거할 수는 없습니다.  
  
 CERTIFICATE *Certificate_name*  
 대칭 키를 암호화하는 데 사용되는 인증서를 지정합니다. 이 인증서는 데이터베이스에 이미 있어야 합니다.  
  
 PASSWORD **='** _password_ **'**  
 대칭 키를 암호화하는 데 사용되는 암호를 지정합니다. *password*는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 실행하는 컴퓨터의 Windows 암호 정책 요구 사항을 충족해야 합니다.  
  
 SYMMETRIC KEY *Symmetric_Key_Name*  
 변경하려는 대칭 키를 암호화하는 데 사용되는 대칭 키를 지정합니다. 이 대칭 키는 데이터베이스에 이미 있어야 하며 열려 있어야 합니다.  
  
 ASYMMETRIC KEY *Asym_Key_Name*  
 변경하려는 대칭 키를 암호화하는 데 사용되는 비대칭 키를 지정합니다. 이 비대칭 키는 데이터베이스에 이미 있어야 합니다.  
  
## <a name="remarks"></a>설명  
  
> [!CAUTION]  
>  데이터베이스 마스터 키의 공개 키 대신 암호를 사용하여 대칭 키를 암호화한 경우 TRIPLE_DES 암호화 알고리즘이 사용됩니다. 따라서 AES와 같은 강력한 암호화 알고리즘을 사용하여 만든 키는 더 약한 알고리즘으로 보호됩니다.  
  
 대칭 키의 암호화를 변경하려면 ADD ENCRYPTION 및 DROP ENCRYPTION 구를 사용합니다. 암호화 없이는 키를 절대로 사용할 수 없습니다. 이러한 이유로 인해 최선의 방법은 이전 암호화 형식을 제거하기 전에 새로운 암호화 형식을 추가하는 것입니다.  
  
 대칭 키의 소유자를 변경하려면 [ALTER AUTHORIZATION](../../t-sql/statements/alter-authorization-transact-sql.md)을 사용합니다.  
  
> [!NOTE]  
>  RC4 알고리즘은 이전 버전과의 호환성을 위해서만 지원됩니다. 데이터베이스의 호환성 수준이 90 또는 100인 경우 새 자료는 RC4 또는 RC4_128로만 암호화할 수 있습니다. 이 옵션은 사용하지 않는 것이 좋습니다. 대신 AES 알고리즘 중 하나와 같은 새 알고리즘을 사용하십시오. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에서 RC4 또는 RC4_128을 사용하여 암호화된 자료는 모든 호환성 수준에서 해독할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 대칭 키에 대한 ALTER 권한이 필요합니다. 인증서 또는 비대칭 키를 통해 암호화를 추가하는 경우 해당 인증서 또는 비대칭 키에 대한 VIEW DEFINITION 권한이 필요합니다. 인증서 또는 비대칭 키를 통해 암호화를 삭제하는 경우 해당 인증서 또는 비대칭 키에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 대칭 키를 보호하는 데 사용되는 암호화 방법을 변경합니다. 대칭 키 `JanainaKey043`은 키가 만들어질 때 인증서 `Shipping04`를 사용하여 암호화됩니다. 키는 암호화되지 않은 상태로 저장될 수 없으므로 암호로 암호화를 추가한 다음 인증서별로 암호화를 제거합니다.  
  
```  
CREATE SYMMETRIC KEY JanainaKey043 WITH ALGORITHM = AES_256   
    ENCRYPTION BY CERTIFICATE Shipping04;  
-- Open the key.   
OPEN SYMMETRIC KEY JanainaKey043 DECRYPTION BY CERTIFICATE Shipping04  
    WITH PASSWORD = '<enterStrongPasswordHere>';   
-- First, encrypt the key with a password.  
ALTER SYMMETRIC KEY JanainaKey043   
    ADD ENCRYPTION BY PASSWORD = '<enterStrongPasswordHere>';  
-- Now remove encryption by the certificate.  
ALTER SYMMETRIC KEY JanainaKey043   
    DROP ENCRYPTION BY CERTIFICATE Shipping04;  
CLOSE SYMMETRIC KEY JanainaKey043;  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [OPEN SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [CLOSE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
