---
title: DECRYPTBYKEYAUTOASYMKEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2015
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOASYMKEY_TSQL
- DECRYPTBYKEYAUTOASYMKEY
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOASYMSKEY function
ms.assetid: 5521d4cf-740c-4ede-98b6-4ba90b84e32d
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a5e036e7c80218750161ffc2322a5969dcbd6e1e
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37784584"
---
# <a name="decryptbykeyautoasymkey-transact-sql"></a>DECRYPTBYKEYAUTOASYMKEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

이 함수는 암호화된 데이터를 암호 해독합니다. 이렇게 하려면 먼저 별도 비대칭 키로 대칭 키를 암호 해독한 다음, 첫 번째 "단계"에서 추출한 대칭 키로 암호화된 데이터를 암호 해독합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DecryptByKeyAutoAsymKey ( akey_ID , akey_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
## <a name="arguments"></a>인수  
 *akey_ID*  
대칭 키 암호화에 사용되는 비대칭 키의 ID입니다. *akey_ID*는 **int** 데이터 형식을 갖습니다.  
  
 *akey_password*  
비대칭 키를 보호하는 암호입니다. *akey_password*는 데이터베이스 마스터 키가 비대칭 개인 키를 보호하는 경우 NULL 값을 가질 수 있습니다. *akey_password*는 **nvarchar** 데이터 형식을 갖습니다.  
  
 *ciphertext* 키로 암호화된 데이터입니다. *ciphertext*는 **varbinary** 데이터 형식을 갖습니다.  
  
 @ciphertext  
대칭 키로 암호화된 데이터를 포함하는 **varbinary** 형식의 변수입니다.  
  
 *add_authenticator*  
원래 암호화 프로세스가 포함되고 암호화된 인증자가 일반 텍스트를 사용하는지 여부를 나타냅니다. 데이터 암호화 프로세스 동안 [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)로 전달된 값과 일치해야 합니다. *add_authenticator*는 암호화 프로세스가 인증자를 사용한 경우 1의 값을 갖습니다. *add_authenticator*는 **int** 데이터 형식을 갖습니다.  
  
 @add_authenticator  
원래 암호화 프로세스가 포함되고 암호화된 인증자가 일반 텍스트를 사용하는지 여부를 나타내는 변수입니다. 데이터 암호화 프로세스 동안 [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)로 전달된 값과 일치해야 합니다. *@add_authenticator*는 **int** 데이터 형식을 갖습니다.
  
 *authenticator*  
인증자의 생성에 대한 기준으로 사용되는 데이터입니다. [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)에 제공된 값과 일치해야 합니다. *authenticator*는 **sysname** 데이터 형식을 갖습니다.  
  
 @authenticator  
인증자가 생성하는 데이터를 포함하는 변수입니다. [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)에 제공된 값과 일치해야 합니다. *@authenticator*는 **sysname** 데이터 형식을 갖습니다.  
  
@add_authenticator  
원래 암호화 프로세스가 포함되고 암호화된 인증자가 일반 텍스트를 사용하는지 여부를 나타내는 변수입니다. 데이터 암호화 프로세스 동안 [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)로 전달된 값과 일치해야 합니다. *@add_authenticator*는 **int** 데이터 형식을 갖습니다.  

*authenticator*  
인증자의 생성에 대한 기준으로 사용되는 데이터입니다. [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)에 제공된 값과 일치해야 합니다. *authenticator*는 **sysname** 데이터 형식을 갖습니다.

@authenticator  
인증자가 생성하는 데이터를 포함하는 변수입니다. [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)에 제공된 값과 일치해야 합니다. *@authenticator*는 **sysname** 데이터 형식을 갖습니다.  

## <a name="return-types"></a>반환 형식  
최대 크기가 8,000바이트인 **varbinary**입니다.  
  
## <a name="remarks"></a>Remarks  
`DECRYPTBYKEYAUTOASYMKEY`는 `OPEN SYMMETRIC KEY`와 `DECRYPTBYKEY` 모두의 기능을 결합합니다. 단일 작업에서 먼저 대칭 키를 해독한 다음, 해당 키를 사용하여 암호화된 텍스트를 해독합니다.  
  
## <a name="permissions"></a>사용 권한  
대칭 키에 대한 `VIEW DEFINITION` 권한 및 비대칭 키에 대한 `CONTROL` 권한이 필요합니다.  
  
## <a name="examples"></a>예
이 예에서는 `DECRYPTBYKEYAUTOASYMKEY`가 암호 해독 코드를 단순화하는 방법을 보여줍니다. 이 코드는 아직 데이터베이스 마스터 키가 없는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 실행해야 합니다.  

```  
--Create the keys and certificate.  
USE AdventureWorks2012;  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'mzkvdMlk979438teag$$ds987yghn)(*&4fdg^';  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'mzkvdMlk979438teag$$ds987yghn)(*&4fdg^';  
CREATE ASYMMETRIC KEY SSN_AKey   
    WITH ALGORITHM = RSA_2048 ;   
GO  
CREATE SYMMETRIC KEY SSN_Key_02 WITH ALGORITHM = DES  
    ENCRYPTION BY ASYMMETRIC KEY SSN_AKey;  
GO  
--  
--Add a column of encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber2 varbinary(128);   
OPEN SYMMETRIC KEY SSN_Key_02  
   DECRYPTION BY ASYMMETRIC KEY SSN_AKey;  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber2  
    = EncryptByKey(Key_GUID('SSN_Key_02'), NationalIDNumber);  
GO  
--Close the key used to encrypt the data.  
CLOSE SYMMETRIC KEY SSN_Key_02;  
--  
--There are two ways to decrypt the stored data.  
--  
--OPTION ONE, using DecryptByKey()  
--1. Open the symmetric key.  
--2. Decrypt the data.  
--3. Close the symmetric key.  
OPEN SYMMETRIC KEY SSN_Key_02  
   DECRYPTION BY ASYMMETRIC KEY SSN_AKey;  
SELECT NationalIDNumber, EncryptedNationalIDNumber2    
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber2))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
CLOSE SYMMETRIC KEY SSN_Key_02;  
--  
--OPTION TWO, using DecryptByKeyAutoAsymKey()  
SELECT NationalIDNumber, EncryptedNationalIDNumber2   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKeyAutoAsymKey ( AsymKey_ID('SSN_AKey') , NULL ,EncryptedNationalIDNumber2))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [OPEN SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY&#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY&#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
