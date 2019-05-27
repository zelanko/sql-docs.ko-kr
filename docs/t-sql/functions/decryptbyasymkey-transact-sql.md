---
title: DECRYPTBYASYMKEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 3a46b3f19bc676b0b8e9f86db684328940b6e520
ms.sourcegitcommit: 83f061304fedbc2801d8d6a44094ccda97fdb576
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/20/2019
ms.locfileid: "65945561"
---
# <a name="decryptbyasymkey-transact-sql"></a>DECRYPTBYASYMKEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 함수는 대칭 키를 사용하여 암호화된 데이터의 암호를 해독합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DecryptByAsymKey (Asym_Key_ID , { 'ciphertext' | @ciphertext }   
    [ , 'Asym_Key_Password' ] )  
```  
  
## <a name="arguments"></a>인수  
 *Asym_Key_ID*  
데이터베이스에 있는 비대칭 키의 ID입니다. *Asym_Key_ID*는 **int** 데이터 형식을 갖습니다.  
  
 *ciphertext*  
비대칭 키로 암호화되는 데이터 문자열입니다.  
  
 @ciphertext  
비대칭 키로 암호화된 데이터를 포함하는 **varbinary** 형식의 변수입니다.  
  
 *Asym_Key_Password*  
데이터베이스에서 비대칭 키를 암호화하는 데 사용되는 암호입니다.  
  
## <a name="return-types"></a>반환 형식  
최대 크기가 8,000바이트인 **varbinary**입니다.  
  
## <a name="remarks"></a>Remarks  
대칭 암호화/암호 해독, 비대칭 키 암호화/암호 해독과 비교하여 비용이 많습니다. 큰 데이터 세트를 작업할 때(예: 테이블에 저장된 사용자 데이터) 개발자는 비대칭 키 암호화/암호 해독을 피하는 것이 좋습니다.  
  
## <a name="permissions"></a>사용 권한  
`DECRYPTBYASYMKEY`는 비대칭 키에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
이 예제에서는 비대칭 키 `JanainaAsymKey02`로 원래 암호화된 암호 텍스트를 해독합니다. `AdventureWorks2012.ProtectedData04`는 이 비대칭 키를 저장했습니다. 이 예제에서는 비대칭 키 `JanainaAsymKey02`로 반환된 데이터를 암호 해독합니다. 예제에서는 암호 `pGFD4bb925DGvbd2439587y`를 사용하여 이 비대칭 키를 암호 해독했습니다. 예제에서는 반환된 일반 텍스트를 **nvarchar** 형식으로 변환했습니다.  
  
```  
SELECT CONVERT(nvarchar(max),  
    DecryptByAsymKey( AsymKey_Id('JanainaAsymKey02'),   
    ProtectedData, N'pGFD4bb925DGvbd2439587y' ))   
AS DecryptedData   
FROM [AdventureWorks2012].[Sales].[ProtectedData04]   
WHERE Description = N'encrypted by asym key''JanainaAsymKey02''';  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [ENCRYPTBYASYMKEY &#40;Transact-SQL&#41;](../../t-sql/functions/encryptbyasymkey-transact-sql.md)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)   
 [ALTER ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)   
 [DROP ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)   
 [암호화 알고리즘 선택](../../relational-databases/security/encryption/choose-an-encryption-algorithm.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
