---
title: DROP COLUMN ENCRYPTION KEY (Transact SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 47208c011acad2d06fdf91cb3762474ca848e23e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-column-encryption-key-transact-sql"></a>DROP COLUMN ENCRYPTION KEY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  데이터베이스에서 열 암호화 키를 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
DROP COLUMN ENCRYPTION KEY key_name [;]  
```  
  
## <a name="arguments"></a>인수  
 *key_name*  
 데이터베이스에서 삭제할 열 암호화 키의 이름이입니다.  
  
## <a name="remarks"></a>주의  
 사용 되는 데이터베이스의 모든 열을 암호화 하는 경우에 열 암호화 키를 삭제할 수 없습니다. 열 암호화 키를 사용 하 여 모든 열을 먼저 삭제 해야 합니다.  
  
## <a name="permissions"></a>Permissions  
 필요한 **ALTER ANY COLUMN ENCRYPTION KEY** 데이터베이스에 대 한 권한이 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-a-column-encryption-key"></a>1. 열 암호화 키를 삭제 하는 중  
 다음 예에서는 라는 열 암호화 키를 삭제 `MyCEK`합니다.  
  
```  
DROP COLUMN ENCRYPTION KEY MyCEK;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [CREATE COLUMN ENCRYPTION KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-column-encryption-key-transact-sql.md)   
 [ALTER COLUMN ENCRYPTION key&#40; Transact SQL &#41;](../../t-sql/statements/alter-column-encryption-key-transact-sql.md)   
 [CREATE COLUMN MASTER KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-column-master-key-transact-sql.md)  
  
  

