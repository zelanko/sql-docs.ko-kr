---
title: DECRYPTBYKEYAUTOASYMKEY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 09/09/2015
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 74aa8bad7e6d848296ef2997017758883226ac48
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbykeyautoasymkey-transact-sql"></a>DECRYPTBYKEYAUTOASYMKEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  대칭 키를 사용하여 해독합니다. 대칭 키는 비대칭 키를 사용하여 자동으로 해독됩니다.  
  
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
 대칭 키 암호화에 사용되는 비대칭 키의 ID입니다. *akey_ID* 은 **int**합니다.  
  
 *akey_password*  
 비대칭 키의 개인 키를 보호하는 암호입니다. 개인 키가 데이터베이스 마스터 키로 보호되는 경우에는 NULL이 될 수 있습니다. *akey_password* 은 **nvarchar**합니다.  
  
 '*암호 텍스트*'  
 키로 암호화된 데이터입니다. *암호 텍스트* 은 **varbinary**합니다.  
  
 @ciphertext  
 형식의 변수는 **varbinary** 키로 암호화 된 데이터가 들어 있는입니다.  
  
 *add_authenticator*  
 인증자가 일반 텍스트와 함께 암호화되었는지 여부를 나타냅니다. 데이터 암호화 시 EncryptByKey로 전달된 값과 같아야 합니다. 인증자가 사용된 경우 1이 됩니다. *add_authenticator* 은 **int**합니다.  
  
 @add_authenticator  
 인증자가 일반 텍스트와 함께 암호화되었는지 여부를 나타냅니다. 데이터 암호화 시 EncryptByKey로 전달된 값과 같아야 합니다.  
  
 *인증자*  
 인증자가 생성될 데이터입니다. EncryptByKey에 제공된 값과 일치해야 합니다. *인증자* 은 **sysname**합니다.  
  
 @authenticator  
 인증자가 생성될 데이터를 포함하는 변수입니다. EncryptByKey에 제공된 값과 일치해야 합니다.  
  
## <a name="return-types"></a>반환 형식  
 **varbinary** 최대 크기가 8, 000 바이트입니다.  
  
## <a name="remarks"></a>주의  
 DecryptByKeyAutoAsymKey는 OPEN SYMMETRIC KEY와 DecryptByKey의 기능을 결합합니다. 단일 작업으로 대칭 키를 해독한 다음 이 키를 사용하여 ciphertext를 해독합니다.  
  
## <a name="permissions"></a>Permissions  
 대칭 키에 대한 VIEW DEFINITION 권한 및 비대칭 키에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `DecryptByKeyAutoAsymKey`를 사용하여 암호를 해독하는 코드를 단순화하는 방법을 보여 줍니다. 이 코드는 아직 데이터베이스 마스터 키가 없는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 실행해야 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [OPEN SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [Encryptbykey&#40; Transact SQL &#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [Decryptbykey&#40; Transact SQL &#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

