---
description: DECRYPTBYKEYAUTOCERT(Transact-SQL)
title: DECRYPTBYKEYAUTOCERT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2015
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECRYPTBYKEYAUTOCERT
- DECRYPTBYKEYAUTOCERT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DECRYPTBYKEYAUTOCERT function
ms.assetid: 6b45fa2e-ffaa-46f7-86ff-5624596eda4a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 73aa01ab2817f9435791af4f2bb01ae81ef86fcc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417439"
---
# <a name="decryptbykeyautocert-transact-sql"></a>DECRYPTBYKEYAUTOCERT(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 함수는 대칭 키로 데이터의 암호를 해독합니다. 해당 대칭 키는 자동으로 인증서의 암호를 해독합니다.  

 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
DecryptByKeyAutoCert ( cert_ID , cert_password   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }   
  [ , { authenticator | @authenticator } ] ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *cert_ID*  
대칭 키 암호화에 사용되는 인증서의 ID입니다. *cert_ID*는 **int** 데이터 형식을 갖습니다.  
  
*cert_password*  
인증서의 프라이빗 키를 암호화하는 데 사용되는 암호입니다. 데이터베이스 마스터 키가 비대칭 프라이빗 키를 보호하는 경우 `NULL` 값을 가질 수 있습니다. *cert_password*는 **nvarchar** 데이터 형식을 갖습니다.  

'*ciphertext*'  
키로 암호화된 데이터 문자열입니다. *ciphertext*는 **varbinary** 데이터 형식을 갖습니다.  

@ciphertext  
키로 암호화된 데이터를 포함하는 **varbinary** 형식의 변수입니다.  

*add_authenticator*  
원래 암호화 프로세스가 포함되고 암호화된 인증자가 일반 텍스트를 사용하는지 여부를 나타냅니다. 데이터 암호화 프로세스 동안 [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)로 전달된 값과 일치해야 합니다. *add_authenticator*는 암호화 프로세스가 인증자를 사용한 경우 1의 값을 갖습니다. *add_authenticator*는 **int** 데이터 형식을 갖습니다.  
  
@add_authenticator  
원래 암호화 프로세스가 포함되고 암호화된 인증자가 일반 텍스트를 사용하는지 여부를 나타내는 변수입니다. 데이터 암호화 프로세스 동안 [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)로 전달된 값과 일치해야 합니다. *\@add_authenticator*는 **int** 데이터 형식을 갖습니다.  
  
*authenticator*  
인증자의 생성에 대한 기준으로 사용되는 데이터입니다. [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)에 제공된 값과 일치해야 합니다. *authenticator*는 **sysname** 데이터 형식을 갖습니다.  
  
@authenticator  
인증자가 생성하는 데이터를 포함하는 변수입니다. [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)에 제공된 값과 일치해야 합니다. *\@authenticator*는 **sysname** 데이터 형식을 갖습니다.  
  
## <a name="return-types"></a>반환 형식  
최대 크기가 8,000바이트인 **varbinary**입니다.  
  
## <a name="remarks"></a>설명  
`DECRYPTBYKEYAUTOCERT`는 `OPEN SYMMETRIC KEY`와 `DECRYPTBYKEY`의 기능을 결합합니다. 단일 작업에서 먼저 대칭 키를 해독한 다음, 해당 키를 사용하여 암호화된 텍스트를 해독합니다.  
  
## <a name="permissions"></a>사용 권한  
대칭 키에 대한 `VIEW DEFINITION` 권한 및 인증서에 대한 `CONTROL` 권한이 필요합니다.   
  
## <a name="examples"></a>예제  
이 예에서는 `DECRYPTBYKEYAUTOCERT`가 암호 해독 코드를 단순화하는 방법을 보여줍니다. 이 코드는 아직 데이터베이스 마스터 키가 없는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스에서 실행해야 합니다.  
  
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
  
  
