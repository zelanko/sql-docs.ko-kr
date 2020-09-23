---
description: ENCRYPTBYASYMKEY(Transact-SQL)
title: ENCRYPTBYASYMKEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ENCRYPTBYASYMKEY
- ENCRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ENCRYPTBYASYMKEY function
- encryption [SQL Server], asymmetric keys
- asymmetric keys [SQL Server], ENCRYPTBYASYMKEY function
ms.assetid: 86bb2588-ab13-4db2-8f3c-42c9f572a67b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 42ffb61535beefeee149124adf7873cce78c1535
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91111090"
---
# <a name="encryptbyasymkey-transact-sql"></a>ENCRYPTBYASYMKEY(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

이 함수는 비대칭 키를 사용하여 데이터를 암호화합니다.  
  
 ![문서 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "문서 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
EncryptByAsymKey ( Asym_Key_ID , { 'plaintext' | @plaintext } )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*asym_key_ID*  
데이터베이스에 있는 비대칭 키의 ID입니다. *asym_key_ID*는 **int** 데이터 형식을 갖습니다.  
  
*일반 텍스트(cleartext)*  
`ENCRYPTBYASYMKEY`는 비대칭 키로 암호화할 데이터 문자열입니다. *cleartext*에는 다음이 있을 수 있습니다
 
+ **binary**
+ **char**
+ **nchar**
+ **nvarchar**
+ **varbinary**
  
또는
  
+ **varchar**
 
데이터 형식입니다.  
  
**\@일반 텍스트(plaintext)**  
`ENCRYPTBYASYMKEY`는 비대칭 키로 암호화할 값을 보유하는 변수입니다. **\@일반 텍스트(plaintext)** 에는 다음이 있을 수 있습니다.
  
+ **binary**
+ **char**
+ **nchar**
+ **nvarchar**
+ **varbinary**
  
또는
  
+ **varchar**
 
데이터 형식입니다.  
  
## <a name="return-types"></a>반환 형식  
최대 크기가 8,000바이트인 **varbinary**입니다.  
  
## <a name="remarks"></a>설명  
비대칭 키를 사용하는 암호화 및 암호 해독 작업은 상당한 리소스를 소비하므로 대칭 키 암호화 및 해독 작업과 비교하여 비용이 많이 듭니다. 개발자는 큰 데이터 세트(예: 데이터베이스 테이블에 저장된 사용자 데이터 세트)에서 비대칭 키 암호화 및 암호 해독 작업을 피하는 것이 좋습니다. 대신 개발자는 먼저 강력한 대칭 키로 해당 데이터를 암호화한 다음, 비대칭 키로 해당 대칭 키를 암호화는 것이 좋습니다.  
  
알고리즘에 따라 입력이 특정 바이트 수를 초과할 경우 `ENCRYPTBYASYMKEY`는 **NULL**을 반환합니다. 특정 제한은 다음과 같습니다.

+ 512비트 RSA 키는 최대 53바이트를 암호화할 수 있습니다.
+ 1024비트 키는 최대 117바이트를 암호화할 수 있습니다.
+ 2048비트 키는 최대 245바이트를 암호화할 수 있습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 인증서와 비대칭 키는 모두 RSA 키에 대한 래퍼로 사용됩니다.  
  
## <a name="examples"></a>예  
이 예에서는 `@cleartext`에 저장된 텍스트를 비대칭 키 `JanainaAsymKey02`로 암호화합니다. 이 명령문은 암호화된 데이터를 `ProtectedData04` 테이블에 삽입합니다.  
  
```sql  
INSERT INTO AdventureWorks2012.Sales.ProtectedData04   
    VALUES( N'Data encrypted by asymmetric key ''JanainaAsymKey02''',  
    EncryptByAsymKey(AsymKey_ID('JanainaAsymKey02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [DECRYPTBYASYMKEY&#40;Transact-SQL&#41;](../../t-sql/functions/decryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
