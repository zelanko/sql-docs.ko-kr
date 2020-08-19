---
description: CERTENCODED(Transact-SQL)
title: CERTENCODED(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CERTENCODED
- CERTENCODED_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CERTENCODED
ms.assetid: 677a0719-7b9a-4f0b-bc61-41634563f924
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: df0a107d49fb04588fb5f607058f57a94fdcc5bc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88367359"
---
# <a name="certencoded-transact-sql"></a>CERTENCODED(Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

이 함수는 인증서의 공개 부분을 이진 형식으로 반환합니다. 이 함수는 인증서 ID를 인수로 가져와서 인코딩된 인증서를 반환합니다. 새 인증서를 만들려면 이진 결과를 **CREATE CERTIFICATE ... WITH BINARY**에 전달합니다.
  
## <a name="syntax"></a>구문  
  
```sql
CERTENCODED ( cert_id )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*cert_id*  
인증서의 **certificate_id**입니다. sys.certificates에서 이 값을 찾습니다. [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)함수도 이를 반환합니다. *cert_id*는 **int** 데이터 형식을 갖습니다.
  
## <a name="return-types"></a>반환 형식
**varbinary**
  
## <a name="remarks"></a>설명  
**CERTENCODED** 및 **CERTPRIVATEKEY**를 함께 사용하여 이진 형태로 인증서의 다른 부분을 반환합니다.
  
## <a name="permissions"></a>사용 권한  
**CERTENCODED**는 누구나 사용할 수 있습니다.
  
## <a name="examples"></a>예제  
  
### <a name="simple-example"></a>간단한 예  
이 예에서는 이름이 `Shipping04`인 인증서를 만든 다음, **CERTENCODED** 함수를 사용하여 인증서의 이진 인코딩을 반환합니다. 이 예에서는 2040년 10월 31일을 인증서 만료 날짜로 설정합니다.
  
```sql
CREATE DATABASE TEST1;
GO
USE TEST1
CREATE CERTIFICATE Shipping04
ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'
WITH SUBJECT = 'Sammamish Shipping Records',
EXPIRY_DATE = '20401031';
GO
SELECT CERTENCODED(CERT_ID('Shipping04'));
  
```  
  
### <a name="b-copying-a-certificate-to-another-database"></a>B. 다른 데이터베이스에 인증서 복사  
조금 더 복잡한 예에서는 `SOURCE_DB` 및 `TARGET_DB`라는 두 데이터베이스를 만듭니다. 그런 다음, `SOURCE_DB`에 인증서를 만들어 `TARGET_DB`에 복사합니다. 마지막으로, `SOURCE_DB`에서 암호화된 데이터가 인증서 사본을 사용하여 `TARGET_DB`에서 해독될 수 있음을 보여 줍니다.
  
예제 환경을 만들려면 `SOURCE_DB` 및 `TARGET_DB` 데이터베이스를 만들고 각 데이터베이스에 마스터 키를 만듭니다. 그런 다음, `SOURCE_DB`에서 인증서를 만듭니다.
  
```sql
USE master;  
GO  
CREATE DATABASE SOURCE_DB;  
GO  
USE SOURCE_DB;  
GO  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'S0URCE_DB KEY Pa$$W0rd';  
GO  
CREATE DATABASE TARGET_DB;  
GO  
USE TARGET_DB  
GO  
CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Pa$$W0rd in TARGET_DB';  
GO  
  
-- Create a certificate in SOURCE_DB  
USE SOURCE_DB;  
GO  
CREATE CERTIFICATE SOURCE_CERT WITH SUBJECT = 'SOURCE_CERTIFICATE';  
GO  
```  
  
다음으로 인증서에 대한 이진 설명을 추출합니다.
  
```sql
DECLARE @CERTENC VARBINARY(MAX);  
DECLARE @CERTPVK VARBINARY(MAX);  
SELECT @CERTENC = CERTENCODED(CERT_ID('SOURCE_CERT'));  
SELECT @CERTPVK = CERTPRIVATEKEY(CERT_ID('SOURCE_CERT'),  
       'CertEncryptionPa$$word');  
SELECT @CERTENC AS BinaryCertificate;  
SELECT @CERTPVK AS EncryptedBinaryCertificate;  
GO  
```  
  
그런 다음, `TARGET_DB` 데이터베이스에서 중복 인증서를 만듭니다. 이 작업을 위해 다음 코드를 수정하여 이전 단계에서 반환된 두 이진 값 @CERTENC 및 @CERTPVK를 삽입합니다. 이 값을 따옴표로 묶지 않습니다.
  
```sql
-- Create the duplicate certificate in the TARGET_DB database  
USE TARGET_DB  
GO  
CREATE CERTIFICATE TARGET_CERT  
FROM BINARY = <insert the binary value of the @CERTENC variable>  
WITH PRIVATE KEY (  
BINARY = <insert the binary value of the @CERTPVK variable>  
, DECRYPTION BY PASSWORD = 'CertEncryptionPa$$word');  
-- Compare the certificates in the two databases  
-- The two certificates should be the same   
-- except for name and (possibly) the certificate_id  
SELECT * FROM SOURCE_DB.sys.certificates  
UNION  
SELECT * FROM TARGET_DB.sys.certificates;  
```  
  
단일 일괄 처리로 실행되는 다음 코드는 `SOURCE_DB`에서 암호화된 데이터를 `TARGET_DB`에서 해독할 수 있음을 보여 줍니다.
  
```sql
USE SOURCE_DB;  
  
DECLARE @CLEARTEXT nvarchar(100);  
DECLARE @CIPHERTEXT varbinary(8000);  
DECLARE @UNCIPHEREDTEXT_Source nvarchar(100);  
SET @CLEARTEXT = N'Hello World';  
SET @CIPHERTEXT = ENCRYPTBYCERT(CERT_ID('SOURCE_CERT'), @CLEARTEXT);  
SET @UNCIPHEREDTEXT_Source =   
    DECRYPTBYCERT(CERT_ID('SOURCE_CERT'), @CIPHERTEXT)  
-- Encryption and decryption result in SOURCE_DB  
SELECT @CLEARTEXT AS SourceClearText, @CIPHERTEXT AS SourceCipherText,   
       @UNCIPHEREDTEXT_Source AS SourceDecryptedText;  
  
-- SWITCH DATABASE  
USE TARGET_DB;  
  
DECLARE @UNCIPHEREDTEXT_Target nvarchar(100);  
SET @UNCIPHEREDTEXT_Target = DECRYPTBYCERT(CERT_ID('TARGET_CERT'), @CIPHERTEXT);  
-- Encryption and decryption result in TARGET_DB  
SELECT @CLEARTEXT AS ClearTextInTarget, @CIPHERTEXT AS CipherTextInTarget, @UNCIPHEREDTEXT_Target AS DecriptedTextInTarget;   
GO  
```  
  
## <a name="see-also"></a>참고 항목
[보안 함수&#40;Transact-SQL&#41;](../../t-sql/functions/security-functions-transact-sql.md)  
[CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)  
[CERTPRIVATEKEY &#40;Transact-SQL&#41;](../../t-sql/functions/certprivatekey-transact-sql.md)  
[sys.certificates&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)
  
  
