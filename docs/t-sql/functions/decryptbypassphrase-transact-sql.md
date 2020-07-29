---
title: DECRYPTBYPASSPHRASE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DECRYPTBYPASSPHRASE
- DECRYPTBYPASSPHRASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- decryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], DECRYPTBYPASSPHRASE function
- DECRYPTBYPASSPHRASE function
ms.assetid: ca34b5cd-07b3-4dca-b66a-ed8c6a826c95
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: e2998d9ff84d7902095620e2e7949985adc3a6b0
ms.sourcegitcommit: 768f046107642f72693514f51bf2cbd00f58f58a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/23/2020
ms.locfileid: "87113006"
---
# <a name="decryptbypassphrase-transact-sql"></a>DECRYPTBYPASSPHRASE(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

이 함수는 원래 암호를 사용하여 암호화된 데이터를 해독합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
DecryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *passphrase*  
암호 해독 키를 생성하는 데 사용된 암호입니다.  
  
 @passphrase  
암호 해독 키를 생성하는 데 사용된 암호를 포함하는 **char**, **nchar**, **nvarchar** 또는 **varchar** 형식의 변수입니다.  
  
'*ciphertext*'  
키로 암호화된 데이터 문자열입니다. *ciphertext*는 **varbinary** 데이터 형식을 갖습니다.  
 
@ciphertext  
키로 암호화된 데이터를 포함하는 **varbinary** 형식의 변수입니다. *\@ciphertext* 변수의 최대 크기는 8,000바이트입니다.  
  
*add_authenticator*  
원래 암호화 프로세스가 포함되고 암호화된 인증자가 일반 텍스트를 사용하는지 여부를 나타냅니다. *add_authenticator*는 암호화 프로세스가 인증자를 사용한 경우 1의 값을 갖습니다. *add_authenticator*는 **int** 데이터 형식을 갖습니다.  
  
@add_authenticator  
원래 암호화 프로세스가 포함되고 암호화된 인증자가 일반 텍스트를 사용하는지 여부를 나타내는 변수입니다. *\@add_authenticator*는 암호화 프로세스가 인증자를 사용한 경우 1의 값을 갖습니다. *\@add_authenticator*는 **int** 데이터 형식을 갖습니다.  

*authenticator*  
인증자의 생성에 대한 기준으로 사용되는 데이터입니다. *authenticator*는 **sysname** 데이터 형식을 갖습니다.  
  
@authenticator  
인증자의 생성에 대한 기준으로 사용된 데이터를 포함하는 변수입니다. *\@authenticator*는 **sysname** 데이터 형식을 갖습니다.  
  
## <a name="return-types"></a>반환 형식  
최대 크기가 8,000바이트인 **varbinary**입니다.  
  
## <a name="remarks"></a>설명  
`DECRYPTBYPASSPHRASE`는 실행에 대한 권한이 필요없습니다. `DECRYPTBYPASSPHRASE`는 잘못된 암호나 잘못된 인증자 정보를 수신하는 경우 NULL을 반환합니다.  
  
`DECRYPTBYPASSPHRASE`는 암호를 사용하여 암호 해독 키를 생성합니다. 이 암호 해독 키는 유지되지 않습니다.  
  
암호 텍스트 암호화의 경우 인증자가 포함되었다면 `DECRYPTBYPASSPHRASE`는 암호 해독 프로세스에 대한 해당 동일 인증자를 받아야 합니다. 암호 해독 프로세스에 제공된 인증자 값이 원래 데이터를 암호화하는 데 사용된 인증자 값과 일치하지 않으면 `DECRYPTBYPASSPHRASE` 작업은 실패합니다.  
  
## <a name="examples"></a>예제  
이 예에서는 [EncryptByPassPhrase](../../t-sql/functions/encryptbypassphrase-transact-sql.md)에서 업데이트된 레코드의 암호를 해독합니다.  
  
```  
USE AdventureWorks2012;  
-- Get the passphrase from the user.  
DECLARE @PassphraseEnteredByUser nvarchar(128);  
SET @PassphraseEnteredByUser   
= 'A little learning is a dangerous thing!';  
  
-- Decrypt the encrypted record.  
SELECT CardNumber, CardNumber_EncryptedbyPassphrase   
    AS 'Encrypted card number', CONVERT(varchar,  
    DecryptByPassphrase(@PassphraseEnteredByUser, CardNumber_EncryptedbyPassphrase, 1   
    , CONVERT(varbinary, CreditCardID)))  
    AS 'Decrypted card number' FROM Sales.CreditCard   
    WHERE CreditCardID = '3681';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [암호화 알고리즘 선택](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ENCRYPTBYPASSPHRASE&#40;Transact-SQL&#41;](../../t-sql/functions/encryptbypassphrase-transact-sql.md)  
  
  
