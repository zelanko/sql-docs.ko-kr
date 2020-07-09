---
title: ENCRYPTBYKEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYKEY_TSQL
- ENCRYPTBYKEY
dev_langs:
- TSQL
helpviewer_keywords:
- authenticators [SQL Server]
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], ENCRYPTBYKEY function
- ENCRYPTBYKEY function
ms.assetid: 0e11f8c5-f79d-46c1-ab11-b68ef05d6787
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 918890142acb736976d642161e2e7cc1f54e3533
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784591"
---
# <a name="encryptbykey-transact-sql"></a>ENCRYPTBYKEY(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  대칭 키를 사용하여 데이터를 암호화합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
EncryptByKey ( key_GUID , { 'cleartext' | @cleartext }  
    [, { add_authenticator | @add_authenticator }  
     , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>인수  
 *key_GUID*  
 *일반 텍스트* 암호화에 사용할 키의 GUID입니다. **uniqueidentifier**  
  
 '*cleartext*'  
 키로 암호화할 데이터입니다.  
  
 @cleartext  
 키로 암호화될 데이터가 들어 있는 **navarchar**, **char**, **varchar**, **이진**, **varbinary** 또는 **nchar** 형식의 변수입니다.  
  
 *add_authenticator*  
 인증자가 *일반 텍스트*와 함께 암호화될지 여부를 나타냅니다. 인증자를 사용하는 경우 1이어야 합니다. **int**  
  
 @add_authenticator  
 인증자가 *일반 텍스트*와 함께 암호화될지 여부를 나타냅니다. 인증자를 사용하는 경우 1이어야 합니다. **int**  
  
 *authenticator*  
 인증자가 파생될 데이터입니다. **sysname**.  
  
 @authenticator  
 인증자가 파생될 데이터를 포함하는 변수입니다.  
  
## <a name="return-types"></a>반환 형식  
 최대 크기가 8,000바이트인 **varbinary**입니다.  
  
 키가 열리지 않거나, 존재하지 않거나, 더 이상 사용되지 않는 RC4 키이며 데이터베이스 호환성 수준이 110 이상이 아닐 경우 Null을 반환합니다.  
 
 *cleartext* 값이 NULL이면 NULL을 반환합니다.
  
## <a name="remarks"></a>설명  
 EncryptByKey는 대칭 키를 사용합니다. 이 키는 열려 있어야 합니다. 대칭 키가 현재 세션에서 이미 열려 있으면 쿼리 컨텍스트에서 다시 열지 않아도 됩니다.  
  
 인증자는 암호화된 필드의 정수 값 대체를 막는 데 유용합니다. 예를 들어 급여 데이터로 이루어진 다음 테이블을 살펴봅니다.  
  
|Employee_ID|Standard_Title|Base_Pay|  
|------------------|---------------------|---------------|  
|345|Copy Room Assistant|Fskj%7^edhn00|  
|697|Chief Financial Officer|M0x8900f56543|  
|694|Data Entry Supervisor|Cvc97824%^34f|  
  
 악의적인 사용자는 암호화 텍스트 저장 컨텍스트에서 암호화를 해제하지 않고도 상당한 정보를 추론할 수 있습니다. Chief Financial Officer는 Copy Room Assistant보다 더 많은 급여를 받으므로 M0x8900f56543으로 암호화된 값이 Fskj%7^edhn00으로 암호화된 값보다 커야 합니다. 이 경우 테이블에 대해 ALTER 권한을 갖는 모든 사용자는 자신의 Base_Pay 필드 데이터를 Chief Financial Officer의 Base_Pay 필드에 저장된 데이터 복사본으로 바꾸어 Copy Room Assistant의 급여를 올릴 수 있습니다. 이러한 전체 값 대체 공격은 암호화를 무시합니다.  
  
 암호화하기 전에 컨텍스트 정보를 일반 텍스트에 추가하여 전체 값 대체 공격을 방지할 수 있습니다. 이러한 컨텍스트 정보는 일반 텍스트 데이터가 이동되지 않았는지 확인하는 데 사용됩니다.  
  
 데이터 암호화 시 인증자 매개 변수가 지정된 경우 DecryptByKey를 사용하여 데이터의 암호를 해독하려면 같은 인증자가 필요합니다. 암호화 시 인증자의 해시는 일반 텍스트와 함께 암호화됩니다. 암호 해독 시 같은 인증자가 DecryptByKey에 전달되어야 합니다. 두 값이 일치하지 않으면 해독에 실패합니다. 이것은 암호화 이후에 해당 값이 이동되었음을 의미합니다. 변화지 않는 고유한 값이 포함된 열을 인증자로 사용하는 것이 좋습니다. 인증자 값이 변경되면 데이터에 액세스하지 못할 수 있습니다.  
  
 대칭 암호화 및 암호 해독은 비교적 속도가 빠르며 대량의 데이터 작업 시 적합합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 암호화 함수를 ANSI_PADDING OFF 설정과 함께 사용하면 암시적 변환으로 인해 데이터가 손실될 수 있습니다. ANSI_PADDING에 관한 자세한 내용은 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)을 참조하세요.  
  
## <a name="examples"></a>예  
 다음 예에 설명된 기능은 [방법: 데이터 열 암호화](../../relational-databases/security/encryption/encrypt-a-column-of-data.md)에서 생성된 키와 인증서에 의존합니다.  
  
### <a name="a-encrypting-a-string-with-a-symmetric-key"></a>A. 대칭 키로 문자열 암호화  
 다음 예에서는 `Employee` 테이블에 열을 추가한 다음 `NationalIDNumber` 열에 저장되는 주민 등록 번호의 값을 암호화합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
  
-- Create a column in which to store the encrypted data.  
ALTER TABLE HumanResources.Employee  
    ADD EncryptedNationalIDNumber varbinary(128);   
GO  
  
-- Open the symmetric key with which to encrypt the data.  
OPEN SYMMETRIC KEY SSN_Key_01  
   DECRYPTION BY CERTIFICATE HumanResources037;  
  
-- Encrypt the value in column NationalIDNumber with symmetric key  
-- SSN_Key_01. Save the result in column EncryptedNationalIDNumber.  
UPDATE HumanResources.Employee  
SET EncryptedNationalIDNumber  
    = EncryptByKey(Key_GUID('SSN_Key_01'), NationalIDNumber);  
GO  
```  
  
### <a name="b-encrypting-a-record-together-with-an-authentication-value"></a>B. 인증 값과 함께 레코드 암호화  
  
```sql 
USE AdventureWorks2012;  
  
-- Create a column in which to store the encrypted data.  
ALTER TABLE Sales.CreditCard   
    ADD CardNumber_Encrypted varbinary(128);   
GO  
  
-- Open the symmetric key with which to encrypt the data.  
OPEN SYMMETRIC KEY CreditCards_Key11  
    DECRYPTION BY CERTIFICATE Sales09;  
  
-- Encrypt the value in column CardNumber with symmetric   
-- key CreditCards_Key11.  
-- Save the result in column CardNumber_Encrypted.    
UPDATE Sales.CreditCard  
SET CardNumber_Encrypted = EncryptByKey(Key_GUID('CreditCards_Key11'),   
    CardNumber, 1, CONVERT( varbinary, CreditCardID) );  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [DECRYPTBYKEY&#40;Transact-SQL&#41;](../../t-sql/functions/decryptbykey-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [DROP SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-symmetric-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [HASHBYTES&#40;Transact-SQL&#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
  
  
