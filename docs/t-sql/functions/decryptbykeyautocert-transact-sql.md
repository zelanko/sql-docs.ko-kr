---
title: DECRYPTBYKEYAUTOCERT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2015
ms.prod: sql
ms.prod_service: sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOCERT
- DECRYPTBYKEYAUTOCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOCERT function
ms.assetid: 6b45fa2e-ffaa-46f7-86ff-5624596eda4a
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3bf53e51d3896953e66e3360aaa810a5c13c51ee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="decryptbykeyautocert-transact-sql"></a>DECRYPTBYKEYAUTOCERT(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  대칭 키를 사용하여 해독합니다. 대칭 키는 인증서를 사용하여 자동으로 해독됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DecryptByKeyAutoCert ( cert_ID , cert_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
## <a name="arguments"></a>인수  
 *cert_ID*  
 대칭 키 암호화에 사용되는 인증서의 ID입니다. *cert_ID*는 **int**입니다.  
  
 *cert_password*  
 인증서 개인 키를 보호하는 암호입니다. 개인 키가 데이터베이스 마스터 키로 보호되는 경우에는 NULL이 될 수 있습니다. *cert_password*는 **nvarchar**입니다.  
  
 '*ciphertext*'  
 키로 암호화된 데이터입니다. *ciphertext*는 **varbinary**입니다.  
  
 @ciphertext  
 키로 암호화된 데이터가 포함된 **varbinary** 형식의 변수입니다.  
  
 *add_authenticator*  
 인증자가 일반 텍스트와 함께 암호화되었는지 여부를 나타냅니다. 인증자가 사용된 경우 data.Is **1**을 암호화할 때 EncryptByKey로 전달된 값과 같아야 합니다. *add_authenticator*는 **int**입니다.  
  
 @add_authenticator  
 인증자가 일반 텍스트와 함께 암호화되었는지 여부를 나타냅니다. 데이터 암호화 시 EncryptByKey로 전달된 값과 같아야 합니다.  
  
 *authenticator*  
 인증자가 생성될 데이터입니다. EncryptByKey에 제공된 값과 일치해야 합니다. *authenticator*는 **sysname**입니다.  
  
 @authenticator  
 인증자가 생성될 데이터를 포함하는 변수입니다. EncryptByKey에 제공된 값과 일치해야 합니다.  
  
## <a name="return-types"></a>반환 형식  
 최대 크기가 8,000바이트인 **varbinary**입니다.  
  
## <a name="remarks"></a>Remarks  
 DecryptByKeyAutoCert는 OPEN SYMMETRIC KEY와 DecryptByKey의 기능을 결합합니다. 단일 작업으로 대칭 키를 해독한 다음 이 키를 사용하여 ciphertext를 해독합니다.  
  
## <a name="permissions"></a>사용 권한  
 대칭 키에 대한 VIEW DEFINITION 권한 및 인증서에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `DecryptByKeyAutoCert`를 사용하여 암호를 해독하는 코드를 단순화하는 방법을 보여 줍니다. 이 코드는 아직 데이터베이스 마스터 키가 없는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 실행해야 합니다.  
  
```  
--Create the keys and certificate.  
USE AdventureWorks2012;  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'mzkvdlk979438teag$$ds987yghn)(*&4fdg^';  
OPEN MASTER KEY DECRYPTION BY PASSWORD = 'mzkvdlk979438teag$$ds987yghn)(*&4fdg^';  
CREATE CERTIFICATE HumanResources037   
   WITH SUBJECT = 'Sammamish HR',   
   EXPIRY_DATE = '10/31/2009';  
CREATE SYMMETRIC KEY SSN_Key_01 WITH ALGORITHM = DES  
    ENCRYPTION BY CERTIFICATE HumanResources037;  
GO  
----Add a column of encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber varbinary(128);   
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037 ;  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber  
    = EncryptByKey(Key_GUID('SSN_Key_01'), NationalIDNumber);  
GO  
--  
--Close the key used to encrypt the data.  
CLOSE SYMMETRIC KEY SSN_Key_01;  
--  
--There are two ways to decrypt the stored data.  
--  
--OPTION ONE, using DecryptByKey()  
--1. Open the symmetric key  
--2. Decrypt the data  
--3. Close the symmetric key  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
SELECT NationalIDNumber, EncryptedNationalIDNumber    
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKey(EncryptedNationalIDNumber))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
CLOSE SYMMETRIC KEY SSN_Key_01;  
--  
--OPTION TWO, using DecryptByKeyAutoCert()  
SELECT NationalIDNumber, EncryptedNationalIDNumber   
    AS 'Encrypted ID Number',  
    CONVERT(nvarchar, DecryptByKeyAutoCert ( cert_ID('HumanResources037') , NULL ,EncryptedNationalIDNumber))   
    AS 'Decrypted ID Number'  
    FROM HumanResources.Employee;  
```  
  
## <a name="see-also"></a>참고 항목  
 [OPEN SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)   
 [ENCRYPTBYKEY&#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [DECRYPTBYKEY&#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
