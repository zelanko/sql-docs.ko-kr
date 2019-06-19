---
title: ASYMKEY_ID(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AsymKey_ID
- ASYMKEY_ID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- asymmetric keys [SQL Server], AsymKey_ID
- ASYMKEY_ID function
- encryption [SQL Server], asymmetric keys
- identification numbers [SQL Server], asymmetric keys
- IDs [SQL Server], asymmetric keys
- cryptography [SQL Server], asymmetric keys
ms.assetid: d697daf8-2106-4ebb-b09a-ca0be465d747
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 48bb97bdf073026ffdc7cde48eac1b295a06bd75
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65944970"
---
# <a name="asymkeyid-transact-sql"></a>ASYMKEY_ID(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

비대칭 키의 ID를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
ASYMKEY_ID ( 'Asym_Key_Name' )  
```  
  
## <a name="arguments"></a>인수  
*Asym_Key_Name*  
데이터베이스에 있는 비대칭 키의 이름입니다.
  
## <a name="return-types"></a>반환 형식
 **ssNoversion**  
  
## <a name="permissions"></a>사용 권한  
비대칭 키에 대한 적절한 사용 권한이 필요하며 비대칭 키에 대한 호출자의 VIEW 권한이 거부되지 않아야 합니다. 비대칭 키 권한에 대한 자세한 내용은 [CREATE ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)를 참조하세요.
  
## <a name="examples"></a>예  
이 예에서는 `ABerglundKey11`이라는 비대칭 키의 ID를 반환합니다.
  
```sql
SELECT ASYMKEY_ID('ABerglundKey11');  
GO  
```  
  
## <a name="see-also"></a>관련 항목:
[CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-asymmetric-key-transact-sql.md)  
[ALTER ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-asymmetric-key-transact-sql.md)  
[DROP ASYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/drop-asymmetric-key-transact-sql.md)  
[SIGNBYASYMKEY&#40;Transact-SQL&#41;](../../t-sql/functions/signbyasymkey-transact-sql.md)  
[VERIFYSIGNEDBYASYMKEY&#40;Transact-SQL&#41;](../../t-sql/functions/verifysignedbyasymkey-transact-sql.md)  
[암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)  
[sys.asymmetric_keys&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md)  
[보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)  
[ASYMKEYPROPERTY&#40;Transact-SQL&#41;](../../t-sql/functions/asymkeyproperty-transact-sql.md)  
[KEY_ID&#40;Transact-SQL&#41;](../../t-sql/functions/key-id-transact-sql.md)
  
  
