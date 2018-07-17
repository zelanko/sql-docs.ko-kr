---
title: DECRYPTBYKEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DecryptByKey_TSQL
- DECRYPTBYKEY
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], DecryptByKey function
- decryption [SQL Server], keys
- decryption [SQL Server], symmetric keys
- DECRYPTBYKEY function
ms.assetid: 6edf121f-ac62-4dae-90e6-6938f32603c9
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 61e984a45f2f5a7b2d675ec574fda255c4747642
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37783064"
---
# <a name="decryptbykey-transact-sql"></a>DECRYPTBYKEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 함수는 대칭 키를 사용하여 데이터의 암호를 해독합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DecryptByKey ( { 'ciphertext' | @ciphertext }   
    [ , add_authenticator, { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>인수  
*ciphertext*  
키로 암호화된 데이터를 포함하는 **varbinary** 형식의 변수입니다.  
  
**@ciphertext**  
키로 암호화된 데이터를 포함하는 **varbinary** 형식의 변수입니다.  
  
 *add_authenticator*  
원래 암호화 프로세스가 포함되고 암호화된 인증자가 일반 텍스트를 사용하는지 여부를 나타냅니다. 데이터 암호화 프로세스 동안 [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)로 전달된 값과 일치해야 합니다. *add_authenticator*는 **int** 데이터 형식을 갖습니다.  
  
 *authenticator*  
인증자의 생성에 대한 기준으로 사용되는 데이터입니다. [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)에 제공된 값과 일치해야 합니다. *authenticator*는 **sysname** 데이터 형식을 갖습니다.  

**@authenticator**  
인증자가 생성하는 데이터를 포함하는 변수입니다. [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)에 제공된 값과 일치해야 합니다. *@authenticator*는 **sysname** 데이터 형식을 갖습니다.  

## <a name="return-types"></a>반환 형식  
최대 크기가 8,000바이트인 **varbinary**입니다. `DECRYPTBYKEY`는 데이터 암호화에 사용되는 대칭 키가 열려 있지 않거나 *ciphertext*가 NULL이면 NULL을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
`DECRYPTBYKEY`는 대칭 키를 사용합니다. 데이터베이스는 이 대칭 키를 이미 열어 두어야 합니다. `DECRYPTBYKEY`는 동시에 여러 개의 키를 열어 둘 수 있습니다. 암호 텍스트를 해독하기 직전에 키를 열 필요는 없습니다.  
  
대칭 암호화 및 암호 해독은 일반적으로 상대적으로 신속하게 작동하고 큰 데이터 볼륨과 관련된 작업에 적합합니다.  
  
## <a name="permissions"></a>사용 권한  
대칭 키는 현재 세션에서 이미 열려 있어야 합니다. 자세한 내용은 [대칭 키 열기&#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)를 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-decrypting-by-using-a-symmetric-key"></a>1. 대칭 키를 사용한 해독  
이 예에서는 대칭 키로 암호 텍스트를 해독합니다.  
  
```  
-- First, open the symmetric key with which to decrypt the data.  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
GO  
  
-- Now list the original ID, the encrypted ID, and the   
-- decrypted ciphertext. If the decryption worked, the original  
-- and the decrypted ID will match.  
SELECT NationalIDNumber, EncryptedNationalID   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalID))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
GO  
```  
  
### <a name="b-decrypting-by-using-a-symmetric-key-and-an-authenticating-hash"></a>2. 대칭 키 및 인증 해시를 사용한 해독  
이 예에서는 인증자를 사용하여 암호화된 데이터를 해독합니다.  
  
```  
-- First, open the symmetric key with which to decrypt the data  
OPEN SYMMETRIC KEY CreditCards_Key11  
   DECRYPTION BY CERTIFICATE Sales09;  
GO  
  
-- Now list the original card number, the encrypted card number,  
-- and the decrypted ciphertext. If the decryption worked,   
-- the original number will match the decrypted number.  
SELECT CardNumber, CardNumber_Encrypted   
    AS 'Encrypted card number', CONVERT(nvarchar,  
    DecryptByKey(CardNumber_Encrypted, 1 ,   
    HashBytes('SHA1', CONVERT(varbinary, CreditCardID))))   
    AS 'Decrypted card number' FROM Sales.CreditCard;  
GO  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [ENCRYPTBYKEY&#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [암호화 알고리즘 선택](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  
