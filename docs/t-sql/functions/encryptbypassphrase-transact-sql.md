---
title: ENCRYPTBYPASSPHRASE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYPASSPHRASE
- ENCRYPTBYPASSPHRASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYPASSPHRASE function
- encryption [SQL Server], symmetric keys
- symmetric keys [SQL Server], ENCRYPTBYPASSPHRASE function
ms.assetid: f8dbb9e6-94d6-40d7-8b38-6833a409d597
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: bf177ff86bbf3fc9f239d9719c956ee5c05a4200
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="encryptbypassphrase-transact-sql"></a>ENCRYPTBYPASSPHRASE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  128비트 키 길이의 TRIPLE DES 알고리즘을 사용하여 전달 구로 데이터를 암호화합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
EncryptByPassPhrase ( { 'passphrase' | @passphrase }   
    , { 'cleartext' | @cleartext }  
  [ , { add_authenticator | @add_authenticator }  
    , { authenticator | @authenticator } ] )  
```  
  
## <a name="arguments"></a>인수  
 *passphrase*  
 대칭 키 생성에 사용할 전달 구입니다.  
  
 @passphrase  
 대칭 키를 생성하는 데 사용할 전달 구가 들어 있는 **nvarchar**, **char**, **varchar**, **binary**, **varbinary** 또는 **nchar** 형식의 변수입니다.  
  
 *cleartext*  
 암호화할 일반 텍스트입니다.  
  
 @cleartext  
 일반 텍스트가 들어 있는 **nvarchar**, **char**, **varchar**, **이진**, **varbinary** 또는 **nchar** 형식의 변수입니다. 최대 크기는 8,000바이트입니다.  
  
 *add_authenticator*  
 인증자가 일반 텍스트와 함께 암호화될지 여부를 나타냅니다. 인증자가 추가되면 1입니다. **int**  
  
 @add_authenticator  
 해시가 일반 텍스트와 함께 암호화되는지 여부를 나타냅니다.  
  
 *authenticator*  
 인증자가 파생될 데이터입니다. **sysname**.  
  
 @authenticator  
 인증자가 파생될 데이터를 포함하는 변수입니다.  
  
## <a name="return-types"></a>반환 형식  
 최대 크기가 8,000바이트인 **varbinary**입니다.  
  
## <a name="remarks"></a>Remarks  
 전달 구는 공백을 포함하는 암호입니다. 전달 구에는 상대적으로 긴 문자열보다 의미 있는 구나 문장이 사용되므로 기억하기가 쉽습니다.  
  
 이 함수는 암호 복잡성은 확인하지 않습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `SalesCreditCard` 테이블의 한 레코드를 업데이트하고 기본 키를 인증자로 사용하여 `CardNumber_EncryptedbyPassphrase` 열에 저장된 신용 카드 번호 값을 암호화합니다.  
  
```  
USE AdventureWorks2012;  
GO  
-- Create a column in which to store the encrypted data.  
ALTER TABLE Sales.CreditCard   
    ADD CardNumber_EncryptedbyPassphrase varbinary(256);   
GO  
-- First get the passphrase from the user.  
DECLARE @PassphraseEnteredByUser nvarchar(128);  
SET @PassphraseEnteredByUser   
    = 'A little learning is a dangerous thing!';  
  
-- Update the record for the user's credit card.  
-- In this case, the record is number 3681.  
UPDATE Sales.CreditCard  
SET CardNumber_EncryptedbyPassphrase = EncryptByPassPhrase(@PassphraseEnteredByUser  
    , CardNumber, 1, CONVERT( varbinary, CreditCardID))  
WHERE CreditCardID = '3681';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [DECRYPTBYPASSPHRASE&#40;Transact-SQL&#41;](../../t-sql/functions/decryptbypassphrase-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
