---
description: DROP SYMMETRIC KEY(Transact-SQL)
title: DROP SYMMETRIC KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP SYMMETRIC KEY
- DROP_SYMMETRIC_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- symmetric keys [SQL Server], removing
- deleting symmetric keys
- encryption [SQL Server], symmetric keys
- removing symmetric keys
- dropping symmetric keys
- cryptography [SQL Server], symmetric keys
- DROP SYMMETRIC KEY statement
ms.assetid: 6150bc67-08cb-402e-9c24-b04c9654b434
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: f07f4d02c005ee89b24a323111c05789dbbd9fac
ms.sourcegitcommit: 7f76975c29d948a9a3b51abce564b9c73d05dcf0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96901046"
---
# <a name="drop-symmetric-key-transact-sql"></a>DROP SYMMETRIC KEY(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  현재 데이터베이스에서 대칭 키를 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
DROP SYMMETRIC KEY symmetric_key_name [REMOVE PROVIDER KEY]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *symmetric_key_name*  
 삭제할 대칭 키의 이름입니다.  
  
 REMOVE PROVIDER KEY  
 EKM(Extensible Key Management) 디바이스에서 EKM 키를 제거합니다. 외부 키 관리에 대한 자세한 내용은 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)를 참조하세요.  
  
## <a name="remarks"></a>설명  
  
EKM(Extensible Key Management) 디바이스의 EKM 키에 비대칭 키를 매핑하고 **REMOVE PROVIDER KEY** 옵션을 지정하지 않으면 데이터베이스에서는 키가 삭제되지만 디바이스에서는 삭제되지 않으며 경고가 발생합니다.  
  
## <a name="permissions"></a>사용 권한  
 대칭 키에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 현재 데이터베이스에서 `GailSammamishKey6`이라는 대칭 키를 제거합니다.  
  
```sql  
CLOSE SYMMETRIC KEY GailSammamishKey6;  
DROP SYMMETRIC KEY GailSammamishKey6;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)   
 [ALTER SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-symmetric-key-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CLOSE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/close-symmetric-key-transact-sql.md)   
 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  
