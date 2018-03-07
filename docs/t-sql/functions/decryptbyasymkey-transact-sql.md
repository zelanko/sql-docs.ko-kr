---
title: DECRYPTBYASYMKEY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- DECRYPTBYASYMKEY
- DECRYPTBYASYMKEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], DECRYPTBYASYMKEY function
- DECRYPTBYASYMKEY function
- decryption [SQL Server], asymmetric keys
ms.assetid: d9ebcd30-f01c-4cfe-b95e-ffe6ea13788b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5c85f80e0b8df4f2e61ad0d5f20e9e5ba4d8b582
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="decryptbyasymkey-transact-sql"></a>DECRYPTBYASYMKEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  비대칭 키를 사용하여 데이터의 암호를 해독합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DecryptByAsymKey (Asym_Key_ID , { 'ciphertext' | @ciphertext }   
    [ , 'Asym_Key_Password' ] )  
```  
  
## <a name="arguments"></a>인수  
 *Asym_Key_ID*  
 데이터베이스에 있는 비대칭 키의 ID입니다. *Asym_Key_ID* 은 **int**합니다.  
  
 *암호 텍스트*  
 비대칭 키로 암호화된 데이터 문자열입니다.  
  
 @ciphertext  
 형식의 변수는 **varbinary** 비대칭 키로 암호화 된 데이터가 들어 있는입니다.  
  
 *Asym_Key_Password*  
 데이터베이스에서 비대칭 키를 암호화하는 데 사용된 암호입니다.  
  
## <a name="return-types"></a>반환 형식  
 **varbinary** 최대 크기가 8, 000 바이트입니다.  
  
## <a name="remarks"></a>주의  
 비대칭 키로 암호화/암호 해독을 수행하면 대칭 키로 암호화/암호 해독을 수행하는 것보다 비용이 훨씬 많이 듭니다. 테이블의 사용자 데이터와 같이 큰 데이터 집합으로 작업할 경우에는 비대칭 키를 사용하지 않는 것이 좋습니다.  
  
## <a name="permissions"></a>Permissions  
 비대칭 키에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `JanainaAsymKey02`에 저장되어 있는 `AdventureWorks2012.ProtectedData04` 비대칭 키로 암호화된 텍스트를 해독합니다. 반환되는 데이터는 `JanainaAsymKey02` 암호로 해독된 `pGFD4bb925DGvbd2439587y` 비대칭 키를 사용하여 해독됩니다. 일반 텍스트 형식으로 변환 됩니다 **nvarchar**합니다.  
  
```  
SELECT CONVERT(nvarchar(max),  
    DecryptByAsymKey( AsymKey_Id('JanainaAsymKey02'),   
    ProtectedData, N'pGFD4bb925DGvbd2439587y' ))   
AS DecryptedData   
FROM [AdventureWorks2012].[Sales].[ProtectedData04]   
WHERE Description = N'encrypted by asym key''JanainaAsymKey02''';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Encryptbyasymkey&#40; Transact SQL &#41;](../../t-sql/functions/encryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [암호화 알고리즘 선택](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
