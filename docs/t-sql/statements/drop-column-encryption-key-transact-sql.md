---
title: DROP COLUMN ENCRYPTION KEY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP COLUMN ENCRYPTION
- DROP COLUMN ENCRYPTION KEY
- DROP_COLUMN_ENCRYPTION_TSQL
- DROP_COLUMN_ENCRYPTION_KEY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DROP COLUMN ENCRYPTION KEY statement
- column encryption key, drop
ms.assetid: 86415302-1383-4d36-9fc7-f780831a2d37
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: f3a17a32fd9b44ea8c2d5fd2de4f9a77375cf227
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47607811"
---
# <a name="drop-column-encryption-key-transact-sql"></a>DROP COLUMN ENCRYPTION KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  데이터베이스에서 열 암호화 키를 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP COLUMN ENCRYPTION KEY key_name [;]  
```  
  
## <a name="arguments"></a>인수  
 *key_name*  
 데이터베이스에서 삭제될 열 암호화 키의 이름입니다.  
  
## <a name="remarks"></a>Remarks  
 데이터베이스의 모든 열을 암호화 하는 데 사용되는 경우 열 암호화 키는 삭제할 수 없습니다. 열 암호화 키를 사용하여 모든 열을 먼저 삭제해야 합니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 **ALTER ANY COLUMN ENCRYPTION KEY** 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-a-column-encryption-key"></a>1. 열 암호화 키 제거  
 다음 예에서는 `MyCEK`이라고 하는 열 암호화 키를 삭제합니다.  
  
```  
DROP COLUMN ENCRYPTION KEY MyCEK;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [CREATE COLUMN ENCRYPTION KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER COLUMN ENCRYPTION KEY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)  
  
  
