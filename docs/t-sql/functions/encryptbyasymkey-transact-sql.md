---
title: ENCRYPTBYASYMKEY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 35
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 711b5887a9411c10c215cc766eb0995c3e056d77
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="encryptbyasymkey-transact-sql"></a>ENCRYPTBYASYMKEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  비대칭 키를 사용하여 데이터를 암호화합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
EncryptByAsymKey ( Asym_Key_ID , { 'plaintext' | @plaintext } )  
```  
  
## <a name="arguments"></a>인수  
 *Asym_Key_ID*  
 데이터베이스에 있는 비대칭 키의 ID입니다. **int**합니다.  
  
 *일반 텍스트*  
 비대칭 키로 암호화될 데이터 문자열입니다.  
  
 **@plaintext**  
 형식의 변수는 **nvarchar**, **char**, **varchar**, **이진**, **varbinary**, 또는 **nchar** 비대칭 키로 암호화 될 데이터가 들어 있는입니다.  
  
## <a name="return-types"></a>반환 형식  
 **varbinary** 최대 크기가 8, 000 바이트입니다.  
  
## <a name="remarks"></a>주의  
 비대칭 키로 암호화 및 암호 해독을 수행하면 대칭 키로 암호화 및 암호 해독을 수행하는 것보다 비용이 훨씬 많이 듭니다. 테이블의 사용자 데이터와 같은 큰 데이터 집합을 암호화하는 경우 비대칭 키를 사용하지 않는 것이 좋습니다. 대신 강력한 대칭 키를 사용하여 데이터를 암호화하고 비대칭 키를 사용하여 대칭 키를 암호화해야 합니다.  
  
 **EncryptByAsymKey** 반환 **NULL** 입력 특정 알고리즘에 따라 바이트 수를 초과 하는 경우. 제한은: 512 비트 RSA 키는 최대 53 바이트를 암호화할 수, 1024 비트 키는 최대 117 바이트를 암호화할 수 있습니다 및 2048 비트 키는 최대 245 바이트를 암호화할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 인증서와 비대칭 키는 모두 RSA 키에 대한 래퍼입니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `@cleartext`에 저장된 텍스트를 비대칭 키 `JanainaAsymKey02`로 암호화합니다. 암호화된 데이터는 `ProtectedData04` 테이블에 삽입됩니다.  
  
```  
INSERT INTO AdventureWorks2012.Sales.ProtectedData04   
    VALUES( N'Data encrypted by asymmetric key ''JanainaAsymKey02''',  
    EncryptByAsymKey(AsymKey_ID('JanainaAsymKey02'), @cleartext) );  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Decryptbyasymkey&#40; Transact SQL &#41;](../../t-sql/functions/decryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  

