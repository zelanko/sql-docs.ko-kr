---
title: DECRYPTBYPASSPHRASE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 28
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0af2f19acced57d722427c8f341db62dbdb34198
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="decryptbypassphrase-transact-sql"></a>DECRYPTBYPASSPHRASE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  전달 구로 암호화된 데이터의 암호를 해독합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DecryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'ciphertext' | @ciphertext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>인수  
 *공유 암호*  
 암호 해독을 위한 키를 생성하는 데 사용할 전달 구입니다.  
  
 @passphrase  
 형식의 변수는 **nvarchar**, **char**, **varchar**, 또는 **nchar** 에 대 한 키를 생성 하는 데 사용 될 전달 구가 들어 있는 암호 해독 합니다.  
  
 '*암호 텍스트*'  
 암호를 해독할 암호화 텍스트입니다.  
  
 @ciphertext  
 형식의 변수는 **varbinary** 암호화 텍스트가 들어 있는입니다. 최대 크기는 8,000바이트입니다.  
  
 *add_authenticator*  
 인증자가 일반 텍스트와 함께 암호화되었는지 여부를 나타냅니다. 인증자가 사용된 경우 1이 됩니다. **int**합니다.  
  
 @add_authenticator  
 인증자가 일반 텍스트와 함께 암호화되었는지 여부를 나타냅니다. 인증자가 사용된 경우 1이 됩니다. **int**합니다.  
  
 *인증자*  
 인증자 데이터입니다. **sysname**합니다.  
  
 @authenticator  
 인증자가 파생될 데이터를 포함하는 변수입니다.  
  
## <a name="return-types"></a>반환 형식  
 **varbinary** 최대 크기가 8, 000 바이트입니다.  
  
## <a name="remarks"></a>주의  
 이 함수를 실행하는 데 필요한 사용 권한은 없습니다.  
  
 잘못된 전달 구나 인증자 정보를 사용하면 NULL을 반환합니다.  
  
 전달 구는 암호 해독 키를 생성하는 데 사용되며 암호 해독 키는 지속형이 아닙니다.  
  
 암호화 텍스트를 생성할 때 인증자를 포함한 경우 암호 해독 시 인증자를 제공해야 합니다. 암호 해독 시 제공한 인증자 값이 데이터를 암호화한 인증자 값과 일치하지 않으면 암호 해독이 실패합니다.  
  
## <a name="examples"></a>예  
 다음 예제에서 업데이트 된 레코드의 암호를 해독 [EncryptByPassPhrase](../../t-sql/functions/encryptbypassphrase-transact-sql.md)합니다.  
  
```  
USE AdventureWorks2012;  
-- Get the pass phrase from the user.  
DECLARE @PassphraseEnteredByUser nvarchar(128);  
SET @PassphraseEnteredByUser   
= 'A little learning is a dangerous thing!';  
  
-- Decrypt the encrypted record.  
SELECT CardNumber, CardNumber_EncryptedbyPassphrase   
    AS 'Encrypted card number', CONVERT(nvarchar,  
    DecryptByPassphrase(@PassphraseEnteredByUser, CardNumber_EncryptedbyPassphrase, 1   
    , CONVERT(varbinary, CreditCardID)))  
    AS 'Decrypted card number' FROM Sales.CreditCard   
    WHERE CreditCardID = '3681';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [암호화 알고리즘 선택](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [ENCRYPTBYPASSPHRASE&#40;Transact-SQL&#41;](../../t-sql/functions/encryptbypassphrase-transact-sql.md)  
  
  
