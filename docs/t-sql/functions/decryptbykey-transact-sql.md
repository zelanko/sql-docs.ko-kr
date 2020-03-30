---
title: DECRYPTBYKEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 9ca108b3336a77becc605040b12c0361db4ac903
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72251372"
---
# <a name="decryptbykey-transact-sql"></a>DECRYPTBYKEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 함수는 대칭 키를 사용하여 데이터의 암호를 해독합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql
  
DecryptByKey ( { 'ciphertext' | @ciphertext }   
    [ , add_authenticator, { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>인수  
*ciphertext*  
키로 암호화된 데이터를 포함하는 **varbinary** 형식의 변수입니다.  
  
**\@ciphertext**  
키로 암호화된 데이터를 포함하는 **varbinary** 형식의 변수입니다.  
  
 *add_authenticator*  
원래 암호화 프로세스가 포함되고 암호화된 인증자가 일반 텍스트를 사용하는지 여부를 나타냅니다. 데이터 암호화 프로세스 동안 [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)로 전달된 값과 일치해야 합니다. *add_authenticator*는 **int** 데이터 형식을 갖습니다.  
  
 *authenticator*  
인증자의 생성에 대한 기준으로 사용되는 데이터입니다. [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)에 제공된 값과 일치해야 합니다. *authenticator*는 **sysname** 데이터 형식을 갖습니다.  

**\@인증자**  
인증자가 생성하는 데이터를 포함하는 변수입니다. [ENCRYPTBYKEY(Transact-SQL)](./encryptbykey-transact-sql.md)에 제공된 값과 일치해야 합니다. *\@authenticator*는 **sysname** 데이터 형식을 갖습니다.  

## <a name="return-types"></a>반환 형식  
최대 크기가 8,000바이트인 **varbinary**입니다. `DECRYPTBYKEY`는 데이터 암호화에 사용되는 대칭 키가 열려 있지 않거나 *ciphertext*가 NULL이면 NULL을 반환합니다.  
  
## <a name="remarks"></a>설명  
`DECRYPTBYKEY`는 대칭 키를 사용합니다. 데이터베이스는 이 대칭 키를 이미 열어 두어야 합니다. `DECRYPTBYKEY`는 동시에 여러 개의 키를 열어 둘 수 있습니다. 암호 텍스트를 해독하기 직전에 키를 열 필요는 없습니다.  
  
대칭 암호화 및 암호 해독은 일반적으로 상대적으로 신속하게 작동하고 큰 데이터 볼륨과 관련된 작업에 적합합니다.  

`DECRYPTBYKEY` 호출은 암호화 키를 포함하는 데이터베이스의 컨텍스트에서 발생해야 합니다. 이를 위해 데이터베이스에 상주하는 개체(예: 보기, 저장 프로시저, 함수)에서 `DECRYPTBYKEY`를 호출합니다. 
  
## <a name="permissions"></a>사용 권한  
대칭 키는 현재 세션에서 이미 열려 있어야 합니다. 자세한 내용은 [대칭 키 열기&#40;Transact-SQL&#41;](../../t-sql/statements/open-symmetric-key-transact-sql.md)를 참조하세요.  
  
## <a name="examples"></a>예  
  
### <a name="a-decrypting-by-using-a-symmetric-key"></a>A. 대칭 키를 사용한 해독  
이 예에서는 대칭 키로 암호 텍스트를 해독합니다.  
  
```sql  
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
  
### <a name="b-decrypting-by-using-a-symmetric-key-and-an-authenticating-hash"></a>B. 대칭 키 및 인증 해시를 사용한 해독  
이 예에서는 인증자를 사용하여 암호화된 데이터를 해독합니다.  
  
```sql  
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

### <a name="c-fail-to-decrypt-when-not-in-the-context-of-database-with-key"></a>C. 키가 있는 데이터베이스의 컨텍스트에 없을 때 암호 해독 실패
다음 예제에서는 키를 포함하는 데이터베이스의 컨텍스트에서 `DECRYPTBYKEY`를 실행해야 함을 설명합니다. `DECRYPTBYKEY`가 마스터 데이터베이스에서 실행될 때 행이 암호 해독되지 않으며 결과는 NULL입니다. 

```sql
-- Create the database
CREATE DATABASE TestingDecryptByKey
GO

USE [TestingDecryptByKey]

-- Create the table and view
CREATE TABLE TestingDecryptByKey.dbo.Test(val VARBINARY(8000) NOT NULL);
GO
CREATE VIEW dbo.TestView AS SELECT CAST(DecryptByKey(val) AS VARCHAR(30)) AS DecryptedVal FROM TestingDecryptByKey.dbo.Test;
GO

-- Create the key, and certificate
USE TestingDecryptByKey;
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'ItIsreallyLong1AndSecured!Passsword#';
CREATE CERTIFICATE TestEncryptionCertificate WITH SUBJECT = 'TestEncryption';
CREATE SYMMETRIC KEY TestEncryptSymmmetricKey WITH ALGORITHM = AES_256, IDENTITY_VALUE = 'It is place for test',
KEY_SOURCE = 'It is source for test' ENCRYPTION BY CERTIFICATE TestEncryptionCertificate;

-- Insert rows into the table
DECLARE @var VARBINARY(8000), @Val VARCHAR(30);
SELECT @Val = '000-123-4567';
OPEN SYMMETRIC KEY TestEncryptSymmmetricKey DECRYPTION BY CERTIFICATE TestEncryptionCertificate;
SELECT @var = EncryptByKey(Key_GUID('TestEncryptSymmmetricKey'), @Val);
SELECT CAST(DecryptByKey(@var) AS VARCHAR(30)), @Val;
INSERT INTO dbo.Test VALUES(@var);
GO

-- Switch to master
USE [Master];
GO

-- Results show the date inserted
SELECT DecryptedVal FROM TestingDecryptByKey.dbo.TestView;

-- Results are NULL because we are not in the context of the TestingDecryptByKey Database
SELECT CAST(DecryptByKey(val) AS VARCHAR(30)) AS DecryptedVal FROM TestingDecryptByKey.dbo.Test;
GO

-- Clean up resources
USE TestingDecryptByKey;

DROP SYMMETRIC KEY TestEncryptSymmmetricKey REMOVE PROVIDER KEY;
DROP CERTIFICATE TestEncryptionCertificate;

Use [Master]
DROP DATABASE TestingDecryptByKey;
GO
```

  
## <a name="see-also"></a>참고 항목  
 [ENCRYPTBYKEY&#40;Transact-SQL&#41;](../../t-sql/functions/encryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [암호화 알고리즘 선택](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)  
  
  
